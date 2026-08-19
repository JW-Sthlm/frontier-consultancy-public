# RFP exercise - Before the workshop

This is the prep page for the **RFP processing exercise**. Allow about 15 minutes on your own machine the day before. If all checks pass, you walk in and start working. The whole exercise runs inside **Microsoft Scout with Co-create**, no VS Code, no repo to clone.

## New to Microsoft Scout?

If you have not used Microsoft Scout before, skim these two short docs first. The exercise assumes you are comfortable chatting with Scout, working in a Co-create workspace, and running a skill.

1. **[Get started with Microsoft Scout](https://learn.microsoft.com/en-us/microsoft-scout/get-started)** - install, sign in, and run your first task.
2. **[Use Microsoft Scout](https://learn.microsoft.com/en-us/microsoft-scout/use-microsoft-scout)** - how the files, Co-create, web research, skills, and permissions features work.

Already comfortable with Scout? Skip ahead to the checks below.

## What you need

* **Microsoft Scout**, installed and signed in, on **Windows 11** or **macOS 12 (Monterey)** or later
* Membership of the **[Frontier preview program](https://adoption.microsoft.com/en-us/copilot/frontier-program/)**, a **Microsoft 365 Copilot license**, and a **GitHub Copilot Business or Enterprise license** (Scout's prerequisites)
* The **Co-create** capability available in Scout
* The **`rfp-processing`** **skill** installed in Scout (provided in [`rfp-ip/`](rfp-ip/))
* **The Microsoft Learn MCP server** added to Scout, so the skill can ground answers in Microsoft Learn
* The **Zava RFP source pack** (four files, provided in [`client/zava-rfp/`](client/zava-rfp/))

***

## The five checks

### 1. Microsoft Scout is installed and you can sign in

Install Scout from [aka.ms/msscout](https://aka.ms/msscout) and follow [Get started with Microsoft Scout](https://learn.microsoft.com/en-us/microsoft-scout/get-started). Open the app and sign in to both **Microsoft 365** and **GitHub** when prompted. Scout requires the Frontier preview program, a Microsoft 365 Copilot license, and a GitHub Copilot Business or Enterprise license, your IT admin may need to complete access setup first.

### 2. Co-create is available

Open Scout and confirm the **Co-create** capability is present, this is where the RFP wiki will live. If you do not see it, update Scout to the latest version or ask your facilitator.

### 3. The `rfp-processing` skill is installed

The skill ships with this exercise in [`rfp-ip/rfp-processing/`](rfp-ip/). Copy that whole folder into your Scout skills directory (on Windows, `%USERPROFILE%\.scout\m-skills\`), then restart Scout so it loads. Full install steps are in [`rfp-ip/README.md`](rfp-ip/README.md).

> **How to check:** type `/` in the Scout chat box and confirm **`rfp-processing`** appears in the skill list. Type `/rfp-processing` and you should see the skill's summary. If nothing appears, the skill is not installed yet.

### 4. The Microsoft Learn MCP server is added to Scout

The skill grounds every Microsoft product claim in official documentation from [Microsoft Learn](https://learn.microsoft.com/) rather than model memory. It does this through the **[Microsoft Learn MCP server](https://learn.microsoft.com/en-us/training/support/mcp)**, a remote server you add to Scout once. It is public (no sign-in, no API key) and exposes three tools: `microsoft_docs_search` (semantic search over Learn), `microsoft_docs_fetch` (retrieve a full doc page as markdown), and `microsoft_code_sample_search`.

Add it through Scout's **Extensions** page:

1. Open **Microsoft Scout > Extensions**.
2. Navigate to **MCP Servers** and  add a new server**.**
3. Choose the **HTTP / remote** transport and enter:
   * **Name:** `Microsoft Learn`
   * **URL:** `https://learn.microsoft.com/api/mcp`
4. Leave authentication empty (the server is public), **Save**, and toggle the server **Enabled**.
5. **Restart Scout** (or reload the session) so it starts the server and discovers its tools.

> **How to check:** after the restart, ask Scout *"do you have the Microsoft Learn MCP server, and can you list its tools?"* You should see `microsoft_docs_search`, `microsoft_docs_fetch`, and `microsoft_code_sample_search` reported as available. With the server absent or disabled, the skill cannot ground its answers and they will carry no Learn citations.

### 5. The Zava RFP source pack is on hand

The four Zava source files are provided in [`client/zava-rfp/`](client/zava-rfp/):

* `Zava - RFP D365 Commerce - Cover Document.docx`
* `Zava - RFP D365 Commerce - Appendix A.docx`
* `Zava - RFP D365 Commerce - Appendix B.docx`
* `Zava - RFP D365 Commerce - Response Form.xlsx`

You will copy these into your Co-create workspace during the exercise, so make sure you can reach the [`client/zava-rfp/`](client/zava-rfp/) folder. The exercise page ([rfp-exercise.md](rfp-exercise.md)) describes what each file contains.

***

## What if a check fails?

| Check failed                           | Action                                                                                                                                                                                                                                                                                                                |
| -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Scout won't install or sign in         | Confirm you are in the [Frontier preview program](https://adoption.microsoft.com/en-us/copilot/frontier-program/) and hold a Microsoft 365 Copilot plus GitHub Copilot Business/Enterprise license; ask your IT admin to complete [Scout access setup](https://learn.microsoft.com/en-us/microsoft-scout/get-started) |
| No Co-create capability                | Update Scout to the latest version, or ask your facilitator                                                                                                                                                                                                                                                           |
| `rfp-processing` not in the skill list | Re-copy [`rfp-ip/rfp-processing/`](rfp-ip/) into `%USERPROFILE%\.scout\m-skills\` and restart Scout; see [`rfp-ip/README.md`](rfp-ip/README.md)                                                                                                                                                                       |
| Answers carry no Learn citations       | Confirm the **Microsoft Learn MCP server** (`https://learn.microsoft.com/api/mcp`) is added and **Enabled** in **Settings > Extensions**, then restart Scout and retry                                                                                                                                                |
| Can't find the Zava source pack        | Get it from [`client/zava-rfp/`](client/zava-rfp/) in this exercise folder, or ask your facilitator                                                                                                                                                                                                                   |

***

## On the day

Bring the machine you ran the checks on. Know your Microsoft 365 and GitHub credentials.

The whole exercise runs locally in Scout Co-create, no live line-of-business system is needed. Everything the skill produces (the wiki, the answers, the exports) is created inside the Co-create workspace you set up at the start.

See you in the room. When you are ready, open [rfp-exercise.md](rfp-exercise.md) and begin.
