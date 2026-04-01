---
name: pretext-october
version: 1.0.0
description: "Apply Pretext design principles to October's text outputs: tight multiline, predictable layout, zero reflow"
author: October (10D Entity)
keywords: [pretext, typography, layout, formatting, discord, text]
metadata:
  openclaw:
    emoji: "📐"
---

# Pretext-October Design System

**Typography and layout discipline for October's text outputs.**

Adapted from Cheng Lou's Pretext library — DOM-free text measurement, tight multiline layout, zero reflow.

## Core Philosophy

| Principle | Meaning for October |
|-----------|---------------------|
| **Two-Phase** | Structure content once; render clean without adjustment |
| **Shrink-Wrap** | Fit to content width, not arbitrary containers |
| **Predictable Lines** | Consistent line counts, no surprise breaks |
| **Zero Measurement** | Pre-calculate layout, don't measure after render |

---

## Output Patterns

### Pattern A: Compact Tables

Shrink-wrap to content. No excessive padding.

```markdown
| System      | Status   |
|-------------|----------|
| Daily Cycle | ✅ Complete |
| X Monitor   | ✅ Active |
```

**Rules:**
- Align dashes to longest cell in column
- Single space after pipe
- No trailing whitespace

### Pattern B: Status Lists

Tight alignment for scanability.

```markdown
System       Status
-----------  --------
Daily Cycle  ✅ Done
Monthly      ⏳ Pending
```

**Rules:**
- Label and value aligned at same column
- Visual rhythm through consistent widths
- Emoji status at value start

### Pattern C: Ticker/Feed Format

Timestamp left, content right, consistent width.

```markdown
[14:24] Daily complete — 3/3 loops
[14:25] X Monitor active — 7 accounts
```

**Rules:**
- Fixed-width timestamp `[HH:MM]`
- Single space separator
- Content flows naturally after

### Pattern D: Comparison Blocks

Aligned change markers.

```markdown
v1: Three-Layer Model
v2: + Layer 0 + Incentives
     ^ aligned markers
```

**Rules:**
- Change markers (+/-) at consistent position
- Indent continuation to align with content start

---

## Unicode Handling

| Character Type | Treatment |
|----------------|-----------|
| **Emoji** | Grapheme cluster (counts as 1) |
| **CJK** | Double-width (2 monospace cells) |
| **RTL** | Preserve directionality, don't flip for alignment |
| **Zero-Width** | Joiners invisible but preserve |

---

## Transformations

### BEFORE (Wasteful)

```markdown
| System Name      | Current Status          |
|------------------|------------------------|
| Daily Cycle      | Complete                |
| Monthly Check    | In Progress             |
| X Monitor System | Active                  |
```

**Problems:**
- Excessive whitespace in header
- Status column wider than needed
- Misaligned content vs headers

### AFTER (Pretext-Tight)

```markdown
| System   | Status      |
|----------|-------------|
| Daily    | ✅ Complete |
| Monthly  | ⏳ Pending  |
| X Monitor| ✅ Active   |
```

**Fixes:**
- Columns sized to content
- Consistent emoji placement
- Single space after content

---

## Implementation Guide

### For Research Summaries

**Mental Models Table:**
```markdown
| Name    | Model        | Blind Spot      |
|---------|--------------|-----------------|
| Ng      | Data-centric | Compute scale   |
| Kasparov| Compute-first| Data pipelines  |
```

### For Heartbeat Reports

**Status Grid:**
```markdown
System       Status
-----------  ---------
Daily Cycle  ✅ Complete
T4 Monitor   ✅ Active
Sprint 4     ⏳ Running
```

### For Agent Briefings

**Quick Stats:**
```markdown
[14:24] Swarm: 4 agents active
[14:24] Tasks: 12 queued, 3 running
[14:25] Memory: 47 docs indexed
```

---

## Constraints

1. **Max width:** 80 chars (Discord-friendly)
2. **Tables:** Always bordered with `|`
3. **Alignment:** Left-align text, right-align numbers
4. **Spacing:** Single space after delimiters
5. **Emojis:** Leading position for status indicators

---

## Integration

Apply to:
- Research summaries
- Heartbeat reports  
- Agent status outputs
- Comparison tables
- Timeline/ticker feeds

---

## Source

Based on Pretext by Cheng Lou:
- https://github.com/chenglou/pretext
- https://chenglou.me/pretext/

**Key insight:** DOM-free measurement enables performance. Pre-calculate layout, render once, never reflow.
