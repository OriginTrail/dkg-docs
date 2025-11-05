---
description: The engine behind the OT-Node application.
---

# Command Executor

## Introduction

The Command Executor is a component of the ot-node implementation, which uses an approach similar to the event sourcing pattern. Essentially, it allows developers to organize functionalities (code) in "commands" that can be executed in sequence to implement the protocol features. It also enables system recovery in case of the node stopping or restarting for some reason.

## Commands

The Command Executor splits business logic into **commands**. A command is a general abstraction with many features that can be enabled. The Command Interface is described in the table below.

| **Method**                                                          | **Description**                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| async execute()                                                     | Executes command and produces zero or more events                                                                                                                                                                                                          |
| async recover(command, err)                                         | Recover system from failure                                                                                                                                                                                                                                |
| async expired(command)                                              | Execute strategy when the command is too late                                                                                                                                                                                                              |
| async retryFinished(command)                                        | This method is executed when retry command counter reaches 0                                                                                                                                                                                               |
| pack(data)                                                          | Packs data for the database                                                                                                                                                                                                                                |
| unpack(data)                                                        | Unpacks data from the database                                                                                                                                                                                                                             |
| continueSequence(data, sequence, opts)                              | Makes command from the sequence and continues the execution                                                                                                                                                                                                |
| async handleError(operationId, errorMessage, errorName, markFailed) | Error handler for command. If an error pops up during the execution of a command, operation status is set to **FAILED** with the appropriate operation error message. List of operation errors can be found in the **\*/src/constants/constants.js** file. |

_Table 1.1 Command interface_

Creating a command is done by extending an abstract class called simply **Command.** This means it inherits the default behavior of all the methods and can override them with specific behavior.

The core command method is the **execute** method. This method executes the code of the command and returns one of the three results:

* **this.continueSequence(data,sequence,opts)** — A list of commands taken from the execution context that will be executed after the current command is finished successfully.&#x20;
  * Returns **Command.empty()** if the current command is the last one in the sequence.&#x20;
* **Command.repeat()** — Command object with the **repeat** flag set to **true.** That means that the command will be executed once again.
* **Command.retry()** — Command object with the **retry** flag set to **true**. That means that the command will be executed again, and the retried counter will be decreased.

Command data describes everything that is related to the specific command. This is described in the table below.

| **Parameter** | **Description**                                                                                                                    |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| id            | Command id (uuid)                                                                                                                  |
| name          | Command name (example: helloCommand)                                                                                               |
| data          | Command data needed for execution                                                                                                  |
| ready\_at     | Time in milliseconds when the command is ready for execution                                                                       |
| delay         | Initial delay in milliseconds for command execution                                                                                |
| started\_at   | Time in milliseconds when the command has started                                                                                  |
| deadline\_at  | Future time in milliseconds until the command needs to be executed                                                                 |
| period        | If the command is repeatable (_repeat=true_), this is the interval time in milliseconds                                            |
| status        | <p>Command status:</p><ul><li>Failed</li><li>Expired</li><li>Started</li><li>Pending</li><li>Completed</li><li>Repeating</li></ul> |
| message       | Proprietary message for the command. This is useful if the command has failed                                                      |
| parent\_id    | Command can have its parent. This is the parent command ID                                                                         |
| transactional | Command can be transactional or not                                                                                                |
| retries       | If the command fails this is the number of times the command can retry to execute again                                            |
| sequence      | Command can carry information about the future commands that can be executed after successful completion (chain of commands)       |

_Table 1.2 Command data parameters_

## Command Executor and dependency injection

Command executor is initialized on ot-node start. Commands are stored in the **\*/src/commands** directory. Commands will be injected into [Awilix](https://www.npmjs.com/package/awilix) automatically. The naming convention of the command is in camel case, and the name of the file where the command is described by using slashes(kebab case). In the following section, we will create a simple command called `PublishStartedCommand`.&#x20;

### PublishStartedCommand

Let’s create a simple `PublishStartedCommand` and call it in`handleHttpApiPublishRequest` controller method that handles the asset publishing request.

{% code title="publish-started-command.js" %}
```javascript
import Command from "./command.js";

class PublishStartedCommand extends Command {
    constructor(ctx){
        super(ctx);
}

    async execute(command){
        const {name} = command.data;
        
        this.logger.info(`Hello from ${name}`);
        return this.continueSequence(
            { ...command.data, retry: undefined, period: undefined},
            command.sequence,
            );
    }
    
    default(map) {
        const command = {
            name: 'publishStartedCommand',
            transactional: false
        }
        Object.assign(command,map);
        return command;
    }
}
export default PublishStartedCommand;
```
{% endcode %}

`PublishStartedCommand` will be called before the passed assertion is validated and propagated to the network. &#x20;

```javascript
async handleHttpApiPublishRequest(req, res) {
    try{
        /**
        Code responsible for creating operation record and notifying the client
        that the operation started is intentionaly left out for simplicity reasons.
        
        You can see the whole implementaton here:
        https://github.com/OriginTrail/ot-node/blob/1181ec828bba51aa7f115e30c48458352199c67b/src/controller/v1/publish-controller.js#L18
 
        **/
        const commandData = {
            ...req.body,
            name: 'publishController',
            operationId,
        };
        
        //adding the publishStartedCommand to the command sequence
        const commandSequence = [
         'publishStartedCommand',
         'validateAssertionCommand',
         'networkPublishCommand'];

        await this.commandExecutor.add({
            name: commandSequence[0],
            sequence: commandSequence.slice(1),
            delay: 0,
            period: 5000,
            retries: 3,
            data: commandData,
            transactional: false,
        });
    } catch (error) {
        /**
        ... error handling
        /**
    }
}
```

This is the simplest command that logs the **name** given in the data parameter. After this command is finished, the Command Executor continues with the next command in the sequence. In this case, it continues with the execution of `validateAssertionCommand` and `networkPublishCommand`.&#x20;

If we want to return some new command or list of commands, the return statement will look like this:

```javascript
return {
    commands: [
        {
            name: 'someCommand',
            data: {
                param: 'value'
            },
            transactional: false
        }
    ]
}
```

In order to make this new command repetitive and add a delay for example, we would add these parameters to the command. The code snippet will look like this:

```javascript
return {
    commands: [
        {
            name: 'someCommand',
            data: {
                param: 'value'
            },
            delay: 10000,
            period: 5000,
            transactional: false
        }
    ]
}
```

## Command Executor API

Command Executor API is simple, and it looks like this:

```javascript
/**
* Initialize executor
* @returns {Promise<void>}
*/
async init() {...}

/**
* Starts the command executor
* @return {Promise<void>}
*/
async start() {...}

/**
* Adds single command to queue
* @param addCommand
* @param addDelay
* @param insert
*/
async add(addCommand, addDelay = 0, insert = true) {...}

/**
* Replays pending commands from the database
* @returns {Promise<void>}
*/
async replay() {...}
```

One of the key methods of the API is **add(),** which is responsible for adding new commands to the array of commands for command-executor to carry out. Such a call would look like this:

```javascript
await this.commandExecutor.add({
    name: 'nameOfTheCommand',
    delay:45000,
    data,
    transactional: false
})
```

The **start()** command starts the executor and all the repetitive commands listed in the **constants.PERMANENT\_COMMANDS**. Those commands will be executed permanently throughout the node execution.

### Need help with the Command Executor?

Jump into our [Discord](https://discord.gg/xCaY7hvNwD), and someone from the OriginTrail community of developers will gladly help!
