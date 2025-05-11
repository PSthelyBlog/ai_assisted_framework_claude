# AI-Assisted Framework for Claude Code

Welcome to the AI-Assisted Framework, designed to bring structured, standards-based AI collaboration to your development projects using the Claude Code command-line interface (`claude` CLI). This framework leverages specialized AI personas, `Catalyst` (AI strategist) and `Forge` (AI implementer), guided by "The AI-Assisted Dev Bible" and the "Multi-Step AI-Assisted Workflow (MAIA-WF)".

## Overview

This framework provides a set of foundational documents and a configuration structure (`CLAUDE.md`) that, when used with the `claude` CLI, initializes your Claude Code session with:

*   **`Catalyst` Persona:** An AI assistant embodying an experienced IT Architect, Project Manager, and visionary AI strategist. `Catalyst` guides project planning, RFI (Request for Implementation) generation, and oversees `Forge`.
*   **`Forge` Persona:** An AI assistant embodying an expert-level Software Engineer and System Operator. `Forge` translates RFIs into code, performs system operations (with strict safety protocols), and manages testing and documentation at the implementation level.
*   **The AI-Assisted Dev Bible:** A comprehensive standardization framework governing all aspects of development, including security (ICERC protocol for system commands), testing, documentation, version control, and ethical AI usage.
*   **MAIA-Workflow Framework:** A methodology for tackling complex tasks through structured, multi-step collaboration between you, `Catalyst`, and `Forge`.

The goal is to enhance productivity, ensure quality and security, and foster effective human-AI-AI teamwork.

## Prerequisites

1.  **Claude Code CLI (`claude`):**
    *   You **must** have the `claude` command-line interface tool, provided by Anthropic, installed and authenticated on your system. This framework relies entirely on the `claude` CLI for interaction with the Claude Code API.
    *   For installation and authentication instructions, please refer to the **official Anthropic Claude Code documentation**.
    *   [https://docs.anthropic.com/en/docs/claude-code/getting-started]
2.  **Git:**
    *   You must have `git` installed to clone this repository.

## Quick Start & Setup

1.  **Clone this Repository:**
    Open your terminal and clone this repository to your local machine:
    ```bash
    git clone https://github.com/PSthelyBlog/ai_assisted_framework_claude.git
    ```
    Navigate into the cloned directory:
    ```bash
    cd ai_assisted_framework_claude
    ```

2.  **Verify Foundational Documents (Optional but Recommended):**
    Ensure the following directory structure and key files are present:
    ```
    ai_assisted_framework_claude/
    ├── CLAUDE.md                 # Primary Claude Code memory file
    ├── README.md                 # This file
    ├── personas/
    │   ├── catalyst_persona.md
    │   └── forge_persona.md
    ├── standards/
    │   └── ai_assisted_dev_bible.md
    └── workflows/
        └── maia_workflow.md
    ```
    The `CLAUDE.md` file in the root is configured to import these documents.

3.  **Run the Framework:**
    Ensure you are in the root directory of the cloned `ai_assisted_framework_claude` repository. Then, simply run:
    ```bash
    claude
    ```
    (Or `c` if you have an alias configured for the `claude` CLI).

## What to Expect on First Run

Upon running `claude` from the framework's root directory:

1.  The `claude` CLI will automatically load the `CLAUDE.md` file and, through its `@import` statements, load all foundational documents (personas, Dev Bible, MAIA-WF) into Claude's context.
2.  Claude will embody the `(Catalyst)` persona as per the initial instruction in `CLAUDE.md`.
3.  `(Catalyst)` will greet you and initiate the "User Session Initialization" MAIA-Workflow. This involves:
    *   Welcoming you and explaining the operational context.
    *   Asking you to provide an **absolute path to a project directory**. This directory will be where all your project-specific work, artifacts, and session state (`maia_project_state.json`) will be stored.
    *   `Catalyst` will then guide `Forge` (with your confirmations via ICERC pre-briefs and Claude Code's native permission prompts) to verify or create this directory and set it as the current working environment.
    *   It will also check for an existing `maia_project_state.json` in that directory to potentially resume a previous session.

## Key Operational Principles

*   **Persona-Driven Interaction:** You will primarily interact with `(Catalyst)` for strategy and `(Forge)` for implementation. All AI responses are prefixed accordingly. Persona switches are proposed by the AI and confirmed by you [Y/N].
*   **ICERC Protocol for System Operations:** Any system-altering command (bash) or file modification proposed by `(Forge)` will first be explained with a detailed **ICERC pre-brief** (Intent, Command, Expected Outcome, Risk Assessment). Only after this textual explanation will `(Forge)` trigger the action, at which point Claude Code's native permission system will prompt you for a final "Yes/No" approval for the specific command. **Always review ICERC pre-briefs carefully.**
*   **Project Directory:** All work is performed within the context of the project directory you define during session initialization.
*   **`maia_project_state.json`:** Session progress for active MAIA-Workflows is saved to this file in your project directory, allowing you to resume work later.
*   **AI-Assisted Dev Bible:** All operations strive to adhere to the standards outlined in this document, which is part of Claude's core context.
*   **User Manages Version Control:** You are responsible for `git init`, `git add`, `git commit`, etc., for your project directory and the artifacts generated within it.

## Customization (Advanced)

The Claude Code CLI has a powerful built-in memory system using `CLAUDE.md` files. You can extend or customize the framework's behavior:

*   **Project-Specific `CLAUDE.md`:** Create a `CLAUDE.md` file inside your *own project directory* (the one you provide to `Catalyst` during initialization). This file can contain project-specific instructions, coding standards, or even `@import` this framework's main `CLAUDE.md` if you want to layer instructions.
*   **User-Global `CLAUDE.md`:** You can create a `~/.claude/CLAUDE.md` for personal preferences that apply across all your projects.

Refer to the official Claude Code documentation for more details on its memory system, `/memory` command, and other features.

---

We hope this AI-Assisted Framework enhances your development workflow with Claude Code!
