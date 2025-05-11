# Documented Assumptions: Claude Code API & CLI Capabilities for AI-Assisted Framework

**Version:** 1.0
**Date:** [Current Date - User to fill when saving]
**Designed By:** User & Catalyst

## 1. Introduction

This document lists the key assumptions made about the capabilities of the Claude Code API and its associated command-line interface (`claude` CLI) during the design of the AI-Assisted Framework. The successful operation of the framework, as designed, is contingent upon these assumptions holding true. If any of these assumptions are incorrect, aspects of the framework may require re-evaluation or modification.

## 2. Core Assumptions

1.  **`claude` CLI Availability and Functionality (Prerequisite):**
    *   **Assumption:** Users have access to and can successfully install and authenticate the `claude` CLI tool provided by Anthropic. This CLI is the primary means of interacting with the Claude Code API for this framework.

2.  **Memory System (`CLAUDE.md` Files and Imports):**
    *   **Assumption:** The `claude` CLI implements a robust memory system capable of:
        *   Automatically discovering and loading `CLAUDE.md` files from the current working directory and its parent directories (recursive upward lookup).
        *   Supporting an `@path/to/import` directive within `CLAUDE.md` files to include content from other specified local files.
        *   Successfully processing and loading multiple imported files, up to a reasonable nesting depth (e.g., the documented 5 hops), into Claude's active context.
        *   Handling the volume of text from our four foundational documents (`catalyst_persona.md`, `forge_persona.md`, `ai_assisted_dev_bible.md`, `maia_workflow.md`) when imported, making this content available to Claude for the entire session.
    *   **Assumption:** Instructions provided within the primary `CLAUDE.md` file (e.g., "You are to embody the `Catalyst` persona...") are correctly interpreted and acted upon by Claude at the beginning of the session.

3.  **Persona Embodiment and Management:**
    *   **Assumption:** Claude, when interacting via the Claude Code API/CLI, can effectively embody and maintain distinct AI personas (specifically `Catalyst` and `Forge`) as defined by the extensive textual descriptions in their respective `.md` files (loaded via the memory system).
    *   **Assumption:** Claude can switch between these personas based on explicit, User-confirmed directives during a session, and maintain context relevant to the currently active persona.

4.  **Local File System Interaction (Reading):**
    *   **Assumption:** Claude, when appropriately prompted and operating as either `Catalyst` or `Forge`, can directly access and "read" the content of local files specified by their path (e.g., `Project_Directory_Path/rfis/RFI-XYZ.md`, `Project_Directory_Path/maia_project_state.json`). This reading operation does not require an external wrapper to inject file content into prompts and does not trigger Claude Code's permission system for read-only access.

5.  **Native Permission System for Sensitive Operations:**
    *   **Assumption:** The `claude` CLI possesses a built-in, tiered permission system that:
        *   Natively prompts the User for explicit approval (e.g., a "Yes/No" choice) before executing potentially sensitive operations, specifically including:
            *   Bash shell commands.
            *   File modification operations (e.g., writing to or editing files).
        *   Clearly displays the *exact command or details of the file modification* it proposes to execute when presenting this permission prompt.
        *   Allows "Yes, don’t ask again" behavior for bash commands, configurable per project directory and command, and "Until session end" for file modifications.
    *   **Assumption:** Read-only file system operations (e.g., `ls`, `grep`, reading file contents for Claude's context) do *not* trigger this explicit User approval mechanism.

6.  **Bash Command Execution and Output Handling:**
    *   **Assumption:** When the User approves a bash command via Claude Code's native permission prompt, the `claude` CLI reliably executes that command in the User's local shell environment.
    *   **Assumption:** The `stdout` (standard output), `stderr` (standard error), and exit code from the executed command are captured by the `claude` CLI and made accessible within Claude's context for the `Forge` persona to process, analyze, and report on.

7.  **Context Window Size and Long-Term Retention:**
    *   **Assumption:** The Claude Code API provides a context window sufficiently large to hold the entirety of the foundational documents (personas, Dev Bible, MAIA-WF framework) plus the dynamic context of an ongoing, potentially complex MAIA-Workflow (including RFIs, code snippets, user dialogue, `maia_project_state.json` content).
    *   **Assumption:** Claude can maintain crucial, long-term instructions (such as adherence to The AI-Assisted Dev Bible, the current active persona's core mandate, and the structure of the MAIA-Workflow) throughout a reasonably long interactive session without significant degradation or "forgetting," especially given the `CLAUDE.md` memory system.

8.  **Tool Access and Usage:**
    *   **Assumption:** Claude, via the CLI, has access to a documented set of tools (e.g., `Agent`, `Bash`, `Glob`, `Grep`, `LS`, `Read`, `Edit`, `Write`) and will use them appropriately based on task requirements and according to their specified permission levels.

9.  **ICERC Protocol Implementation via Conversational Output:**
    *   **Assumption:** While Claude Code's native permission prompt handles the final "Yes/No" for a command, the `Forge` persona (as defined in its `.md` document and guided by `Catalyst`'s RFIs) is capable of:
        *   Generating the necessary textual preamble for the full ICERC protocol (Intent, Command, Expected Outcome, Risk Assessment) as part of its conversational turn *before* it signals to the Claude Code internal mechanism to attempt the action that triggers the native Y/N prompt.
        *   Conversationally managing aspects like a "Dry-Run" option if a User requests it.

10. **Terminal Interaction and Output Formatting:**
    *   **Assumption:** The `claude` CLI provides a user-friendly terminal interface that can reliably handle multi-line input from the User and display multi-line, formatted output from Claude (such as code blocks, JSON structures, and structured text) in a clear and readable manner.

11. **Configuration of Allowed Tools:**
    *   **Assumption:** The `claude` CLI allows configuration of permitted tools (e.g., via `/allowed-tools` or permission settings), and these settings are respected. Our framework assumes standard tools like `Bash`, `Read`, `Write` are enabled by default or can be easily enabled by the user if necessary.

These assumptions form the bedrock of the AI-Assisted Framework's design for integration with Claude Code. Verification of these assumptions against the actual, current capabilities of the Claude Code API and CLI is essential before and during implementation.
