---
description: >-
  Having issues? This page provides solutions to common errors, setup problems,
  and runtime issues, helping you quickly get your DKG Node back online and
  fully functional.
---

# Troubleshoot

#### Authentication issues

**If you run into Browser login problems while working on your project, try the following**

* Navigate to login:
  * `http://localhost:9200/login`
  * or `http://localhost:8081/login` (dev mode)
* Open browser dev tools (right-click → Inspect) → **Console** tab
*   Run:

    ```js
    localStorage.clear()
    ```
* Refresh page

Root cause: switching DB setups can leave stale `clientId` values in cache.

**If you have trouble with Cursor accessing your DKG Node MCP server, perform a Cursor authentication reset**

* Go to **Settings → Tools & Integrations**
* Find your MCP server → click **Disabled**
* Select **Logout** in the pop-up

**Similarly, VS Code authentication reset**

* Open **Command Palette (Ctrl/Cmd + Shift + P)**
* Select **Authentication: Remove Dynamic Authentication Providers**
* Choose your MCP server → OK → Remove

***

### Best practices

#### Effective agent interaction

* Be specific in your queries
* Upload relevant documents before asking questions
* Use follow-up questions to refine responses

#### Security considerations

* Regularly review **user permissions & scopes**
* Monitor **authentication logs** for anomalies
* Keep your **OAuth 2.1 credentials** secure
* Use **dev mode only** in safe environments

***

With the DKG Node interfaces, you can:

* **Log in securely** to your DKG Node via OAuth 2.1
* **Chat naturally** with your DKG Node Agent
* **Invoke tools** from DKG Essentials and your custom plugins to interact with the DKG
* **Integrate external agents** (MCP clients like Cursor or VS Code) to be powered by your DKG Node
* **Explore your APIs** and test exposed tools through Swagger

✨ Your DKG Node and agent are the gateway to **creating and consuming verifiable knowledge** on the DKG. 🚀

> **No results yet?**\
> Publishing can take up to a minute, sometimes it's a short wait.

> **Wrong blockchain or DKG Node engine?**\
> Ensure **OT-Node URL** and **chain name** in your `.env` are exactly:
>
> * `https://v6-pegasus-node-02.origin-trail.network/`
> * `otp:20430`

> **Wallet issues?**\
> Verify test **TRAC** and **NEURO** balances on **NeuroWeb testnet Subscan**.

> **Env vars not picked up?**\
> Confirm values in `apps/agent/.env`. Restart `npm run dev` after changes.
