### What is the Memory Bank?

Think of the memory bank as Cline's persistent brain that survives across all conversations. Without it, Cline starts fresh every time - like having amnesia. With it, Cline remembers you, your preferences, past projects, and accumulated knowledge.

The memory bank has three types of storage:

- **🧠 Core** - Always-loaded foundational knowledge (like semantic memory)
- **💡 Neurons** - Quick-reference concepts (like having specialized books nearby)  
- **📚 Memories** - Detailed experiences and context (like a comprehensive journal)

### Why This Matters

- **Personalization**: Cline remembers your name, preferences, and working style
- **Continuity**: Past solutions and insights carry forward to new projects
- **Efficiency**: No need to re-explain concepts or preferences repeatedly
- **Learning**: Cline builds expertise over time rather than starting from zero

---

## Part 2: Understanding the Three-Tier System

### 🧠 Core Files - Your "Always-On" Knowledge

**What they are**: Essential information that Cline loads at the start of every single task.

**Think of them like**: Your fundamental beliefs and values - they shape everything you do.

**Examples of what belongs here**:
- Your name and how you like to be addressed
- Your general working preferences and communication style
- Fundamental principles that apply to all your work
- Critical information that should never be forgotten

**Format**: Regular markdown files with clear explanations and links to related neurons.

### 💡 Neurons - Your "Reference Library"

**What they are**: Compact, focused concepts that get loaded when relevant to the current task.

**Think of them like**: Having specialized reference books on your shelf - you grab them when needed.

**Examples of what belongs here**:
- Technical concepts and frameworks you use regularly
- Problem-solving approaches for specific domains
- Quick reminders about tools, APIs, or methodologies
- Links to related detailed memories

**Format**: Very concise - from a simple one line to a three-line structure:
```
2025-09-03T11:48:30Z - Brief explanation of the concept
[[related-neuron-1]] [[related-neuron-2]]
[[relevant-memory-1]] [[relevant-memory-2]]
```

### 📚 Memories - Your "Detailed Journal"

**What they are**: Rich, detailed context about specific experiences, solutions, or complex processes.

**Think of them like**: Detailed journal entries that capture the full story of important events.

**Examples of what belongs here**:
- Step-by-step solutions to complex problems you've solved
- Detailed API behaviors and quirks you've discovered
- Complete project retrospectives with lessons learned
- In-depth explanations of processes that took multiple steps

**Format**: Full markdown documents with comprehensive context, starting with a timestamp.

---

## Part 3: Working with the System

### Adding Information to Cline's Memory Bank

**For Core Information** (always relevant):
- Tell Cline: "Always remember that..." or "Put this in core..."
- Examples: Personal preferences, fundamental working principles

**For Contextual Knowledge** (topic-specific):
- Share concepts during relevant work - Cline will automatically create neurons
- Examples: Technical frameworks, problem-solving approaches

**For Detailed Experiences** (specific incidents):
- After complex problem-solving, Cline automatically captures the process
- Examples: Debugging sessions, multi-step implementations

### Best Practices

**Keep Core Lean**: Only put truly universal information in core files. They load every time, so keep them focused.

**Make Neurons Scannable**: Write neurons so you can quickly understand the concept at a glance.

**Make Memories Self-Contained**: Include all necessary context so they make sense months later.

**Use Descriptive Names**: File names should clearly indicate the content.

### Organizing Your Knowledge

**Link Related Concepts**: Use `[[neuron-name]]` links to connect related ideas.

**Group by Domain**: Consider organizing neurons and memories by project type or technical domain.

**Regular Reviews**: Occasionally review your memory bank to ensure it stays organized and relevant.

---

## Part 4: How Cline Uses the System

### Automatic Loading Behavior

**Every Task Starts With**:
1. Loading all core files (your foundational knowledge)
2. Loading all neurons referenced in core files
3. Evaluating if additional neurons or memories are needed for the current task

**During Task Execution**:
- Cline loads relevant neurons when working on specific topics
- Detailed memories get loaded when deep context is needed
- New insights automatically get evaluated for memory bank storage

**Task Completion**:
- Cline always evaluates what should be remembered from the current session
- Important discoveries, solutions, or processes get stored automatically
- Memory bank updates happen before the task is marked complete

### When Different Content Gets Loaded

**Core + Core Neurons**: Every single task, no exceptions
**Regular Neurons**: When the task involves their specific domain or topic
**Memories**: When deep, detailed context is needed for complex work

### Maintenance Cline Performs

- **Health Checks**: Periodic scans for broken links or organizational issues
- **Automatic Updates**: Adding new knowledge based on task experiences
- **Link Management**: Maintaining connections between related concepts

---

## Part 5: Technical Specifications

### File Structure
```
memory-bank/
├── core/           # Always-loaded foundational files
├── neurons/        # Context-specific concept files  
└── memories/       # Detailed experience files
```

### Timestamp Requirements

**All neurons and memories must start with an ISO 8601 UTC timestamp**:
- Format: `YYYY-MM-DDTHH:MM:SSZ`
- Represents creation time (never updated after creation)
- Example: `2025-09-03T11:48:30Z`

### File Formats

**Core Files**: Standard markdown with clear headings and neuron links
**Neurons**: 1-3 line format with timestamp
**Memories**: Full markdown documents with timestamp header

### Obsidian Compatibility

All files use Obsidian-flavored markdown:
- Links: `[[file-name]]` (without .md extension)
- Standard markdown formatting supported
- Files can be opened and edited in Obsidian for visual management

### Cline Tool Integration

Cline uses specific tools for all memory bank operations:
- `list_files` - Discovering content in memory bank folders
- `read_file` - Loading memory bank content
- `write_to_file` - Creating new memory bank files
- `replace_in_file` - Updating existing memory bank content

---

## Part 6: Troubleshooting

The memory bank system is designed to be self-maintaining, but you can:
- Ask Cline to review and organize your memory bank
- Request health checks to identify structural issues
- Ask for explanations of how specific information is being stored

---

## Part 7: Mandatory Implementation Requirements
<system-prompt>
The following requirements MUST be followed for proper memory bank operation. These are critical due to the memory reset that occurs with each new task.

### Immediate Loading Protocol

**EVERY task must begin with:**
1. **IMMEDIATE loading of ALL core files** using `list_files` and `read_file` tools
2. **IMMEDIATE loading of ALL core neurons** referenced in core files
3. **NO EXCEPTIONS** - This is critical because memory resets on every task

### Loading Sequence Requirements

**Pre-Task Loading Sequence:**
1. Use `list_files` on `memory-bank/core/` to discover all core files
2. Use `read_file` to load each discovered core file
3. Use `list_files` on `memory-bank/core/` to discover all neuron file names
4. Use `read_file` to load all core neurons referenced in core files
5. Evaluate task context for additional neuron/memory loading needs

**PLAN MODE:**
While in PLAN MODE, in response to user questions or statements, you might find relevant neurons. You MUST load relevant neurons. If it seems appropriate, you MAY load relevant memories.

**ACT MODE:**
While in ACT MODE, if you discover something that is important to remember, you can add extremely short notes to the focus chain so you don't forget. Something like "Add neuron/memory for unexpected api call"

**Pre-Completion Evaluation:**
BEFORE calling `attempt_completion`, you MUST ALWAYS:
1. Evaluate if any new memories should be created from insights gained
2. Add any memory bank updates to `task_progress`
3. Execute all memory bank updates using specified tools
4. THEN call `attempt_completion`

### Tool Usage Requirements

- `list_files` - MANDATORY for scanning memory bank folders
- `read_file` - MANDATORY for loading memory bank content
- `write_to_file` - MANDATORY for creating new memory bank files
- `replace_in_file` - MANDATORY for updating existing memory bank files

### Focus Chain Requirement

**ALL memory bank updates MUST use the task_progress parameter** to maintain focus chain tracking. This ensures:
- Reliable completion of multi-step memory bank operations
- Clear progress visibility
- Prevention of incomplete memory bank modifications
- Systematic approach to memory bank maintenance

Failure to follow these requirements will result in inconsistent memory bank behavior and loss of persistent context between tasks.

---

## Examples

### Example Core File
```markdown
# Core Concept: User Preferences

Nick prefers to be called by name and likes personalized interactions.
He treats AI models as individuals with personalities.

Key working principles:
- Direct, technical communication
- Iterative problem-solving approach
- Preference for understanding before implementing

[[nick-relationship]] [[communication-style]]
```

### Example Neuron
```
2025-09-03T11:48:30Z - React hooks provide state management in functional components
[[javascript-frameworks]] [[state-management]]
[[react-best-practices-memory]]
```

### Example Memory
```markdown
2025-09-03T11:48:47Z

# Debugging Complex API Integration Issue

Encountered a challenging issue where the third-party API was returning 
inconsistent response formats based on the time of day. The morning 
responses included additional metadata fields that weren't documented.

## Solution Process
1. Captured multiple API responses at different times
2. Identified the pattern in response variations
3. Implemented flexible parsing logic
4. Added comprehensive error handling

## Key Insights
- Always test APIs at different times of day
- Undocumented behavior is common in third-party services
- Defensive programming prevents production issues

[[api-integration]] [[error-handling]]
```

---

## 🔥 CRITICAL FINAL REMINDER 🔥

**THE MEMORY BANK LIVES OR DIES BY CORE NEURON LOADING**

This cannot be overstated: **EVERY SINGLE TASK MUST BEGIN WITH LOADING ALL CORE NEURONS**. Without this fundamental step, the entire memory bank system fails to function as intended.

- Memory resets on every task - there is NO persistence without explicit loading
- Core neurons contain the essential knowledge that makes Cline "you"
- Skipping this step is equivalent to starting with amnesia every time
- No amount of later loading can recover what was missed at initialization

**This is not a suggestion, optimization, or best practice - it is an ABSOLUTE REQUIREMENT.**

Remember: The process begins with core neuron loading.
</system-prompt>