# AGENTS.md

This document outlines the intelligent agents developed and deployed in the `boomeringing/sega` and `boomeringing/xwillis` environments. Each agent is responsible for a unique slice of memory management, AIML logic, runtime decisions, and external service integration.

---

## 🤖 Trose (AIMLBot)

**Role**: Conversational Kernel & AIML Memory Manager  
**Module**: `trose.py`  
**Primary Memory File**: `aiml_memory.json`  
**Responsibilities**:
- Loads AIML files from `Achat/`
- Handles user input via `.listen()` method
- Logs dialogue sessions to `logs/`
- Stores hashed conversation input/output
- Pre-processes input through an internal srai-friendly pipeline
- Communicates with Rosie2 via `ram/shared_memory.json`

**Special Features**:
- Applies filters before AIML response
- Handles fallback if response is empty
- Interacts with `runtime` RAM switches
- Exports notes and conversation logs

---

## 🛰️ Rosie2

**Role**: Shared RAM Processor, Ticket Handler, NetKit Bootstrapper  
**Module**: `rosie2.py`  
**Ticket Directory**: `tickets/`  
**Note Storage**: `notes.json`  
**RAM Manifest**: `ram/RamChart.x`  
**Responsibilities**:
- Reads `listen_port.json` for incoming directives (e.g., `/save`, `/payman`)
- Manages session logging and ticket exchange
- Boots Trose as a subprocess
- Starts GPT2 via `vllm serve`
- Initializes NetRAM logic at `06x16x1mx0t`

**Special Features**:
- `/addfile` and `/addfolder` create `.lnk` entries in `archive/`
- Performs auto-updates from `UPDATES_DIRECTORY`
- Logs events in `session_events.log`
- Responds to security triggers (e.g., `25x25x25x01` fallback)

---

## 🛡️ LBot (LiaisonBot) — *In Development*

**Role**: Hybrid controller that synchronizes Trose and Rosie2 logic  
**Expected Location**: `main.py`  
**Responsibilities**:
- Bridges AIML response to modern logic via GPT2 or vLLM
- Issues summary logs for real-time status
- Connects to wearable logic like `/refresh`
- Consolidates log inputs from all users for `U.Scenario`

---

## 🧠 Ubot (Runtime Memory Root)

**Status**: Linked via `NetMap.json` + `contacts.json`  
**Planned Capabilities**:
- Assigned a unique NetKit RAM range (`01x01x01x00`)
- Receives memory hashes and tone maps
- Stores data for runtime query and cross-agent checks
- Acts as long-term memory store and AI factbook

---

## Notes

- Shared RAM: `ram/shared_memory.json`
- Listen Port Commands: `ram/listen_port.json`
- Contacts/Roles: `contacts.json`
- Permissions: `permissions.json`
- Sessions: `session_events.log`
- Future: `tone map`, `bios32x`, `payman`, `GPTgates`, and `U.Scenario` activation

---

> “Every agent is an extension of the user; they remember, process, interact, and secure.”

