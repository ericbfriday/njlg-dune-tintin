# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a TinTin++ script collection for [Dune MUD](http://dunemud.com/). TinTin++ is a MUD client that uses `.tin` files for scripting automation, triggers, aliases, and actions.

## Running the Scripts

```bash
# Linux/BSD/macOS
tt++ -r main.tin

# Windows (WinTin++)
# Open WinTin++ and run: #read main.tin
```

## Architecture

### Entry Point
`main.tin` loads all library modules and then the character file.

### Directory Structure
- `lib/` - Core functionality shared across all characters
- `guilds/` - Guild-specific combat scripts and abilities
- `characters/` - Per-character configuration (login credentials, guild selection, loop paths)
- `maps/` - Location maps (planned)
- `paths/` - Path definitions for automated movement loops (planned)

### Core Modules (lib/)

**general.tin** - Core automation:
- Combat state tracking (`$attacking`, `$autoAttack`)
- Health/CP/EP prompt parsing via `#action` triggers
- Auto-attack system that matches mob names from `$mobs` list
- Corpse handling delegation (calls guild-specific `handleCorpse`)
- Auto-loot triggers for solaris and items

**looper.tin** - Path walking automation:
- `startLoop` / `stopLoop` / `continueLoop` aliases
- Uses `$loopPath` variable set by character file
- Pauses walking during combat (`$attacking` check)

**loops.tin** - Predefined movement paths:
- Variables like `$loop.arrakis.AbandonedSietch`, `$loop.tleilaxu.noobWest`
- Semicolon-separated directional commands

**mobs.tin** - Mob definitions:
- `$mobs` list (full names for pattern matching)
- `$mobsShortnames` list (for attack commands)
- Lists must be kept in sync (same index = same mob)

### Guild Scripts (guilds/)

Each guild file must define:
- `handleCorpse` alias - guild-specific corpse processing
- `attack` alias - guild-specific attack sequence

**atreides.tin** - Atreides guild: shieldbelt armor, powerwords stun, righteous fury buff, counterstrike (GL 20+), aid healing, request supplies
**fremen.tin** - Fremen guild: degland/distill corpse, weirding ability, poison crysknife
**tleilaxu.tin** - Tleilaxu guild: process/transfuse corpse, backstab, dart throwing, confuse ability

### Character Setup

Copy `characters/example.tin` and configure:
1. Session credentials: `#session {dune} dunemud.net 6789; <Name>; <Password>;`
2. Guild include: `#read guilds/<guild>.tin`
3. Loop path: `#variable {loopPath} {$loop.<planet>.<area>}`

## TinTin++ Syntax Reference

- `#variable {name} {value}` - Set variable
- `$varname` - Reference variable
- `#action {pattern} {commands}` - Trigger on text pattern
- `#alias {name} {commands}` - Create command alias
- `#ticker {name} {commands} {seconds}` - Recurring timer
- `#send {text}` - Send raw command to MUD
- `#if {condition} {then} {else}` - Conditional
- `#nop` - Comment
- `%1`, `%2`, etc. - Capture groups in action patterns
- `%d` - Match digits, `%*` - Match anything

## Newbie Leveling Areas Reference

**Caladan has NO level 1-5 area.** Atreides players must travel to other planets for early leveling.

| Planet | Area | Level | Directions from AP |
|--------|------|-------|-------------------|
| Giedi Prime | The Infirmary | 1-5 | `all e` |
| Wallach IX | Orchard | 1-50 | `5n, enter` |
| Wallach IX | Wallach Ward | newbie | `e,e,down` |
| Caladan | Atreides High School | 5-20 | `3w, n` |
| Caladan | Forest Brigand Camp | 10-20 | `6e, all n, 2w, squeeze` (level 10 cap) |
| Caladan | Smuggler's Cave | 15-20 | `all w, climb down, move bush` (need torch) |

See `dunemud-llm-kb.txt` for comprehensive DuneMUD game mechanics and guild information.
