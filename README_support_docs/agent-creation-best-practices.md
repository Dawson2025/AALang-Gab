---
resource_id: "721ca1c0-71ac-4177-99ba-b9a7b9c7001c"
---
# GAB Tool Best Practices

This document provides actionable best practices for creating stable GAB agents that require fewer modifications and bug fixes. Follow these patterns from the start to build more robust agents.

<!-- section_id: "2df5ecca-fe73-4731-bcd3-7923f9c14ac0" -->
## Why These Practices Matter

GAB agents are complex systems with multiple actors, personas, modes, and state management components. Without careful design, small inconsistencies or implicit assumptions can lead to unpredictable behavior, requiring multiple rounds of debugging and modification. The practices in this document are derived from real-world development cycles where agents required 10+ iterations to fix issues that could have been prevented with upfront planning.

**What happens when you follow these practices:**

- **Reduced modification cycles**: Agents that follow these practices typically require 2-3 modification cycles instead of 10+. Issues are caught during development rather than after deployment.
- **Predictable behavior**: Explicit instructions and consistent patterns ensure the agent behaves the same way every time, making it easier to debug when issues do arise.
- **Faster development**: Spending time upfront on consistency, explicit instructions, and error handling saves significant time later when you don't have to track down why the agent did something unexpected.
- **Better user experience**: Clear separation between internal operations and user-facing messages, proper error handling, and well-designed communication patterns create a more polished, professional agent.
- **Easier maintenance**: When you need to update your agent, consistent patterns and explicit instructions make it clear where changes need to be made and ensure you don't miss related sections.

---
<!-- section_id: "3d17965b-f909-4ebc-b505-05f9921a235d" -->
## Key Principles to Follow
Using the GAB tool well helps you emphasise these postitives.

<!-- section_id: "be43e5e2-07d7-4e32-af8a-e33b8833515a" -->
### 1. **Explicit Over Implicit**
Always prefer explicit instructions over implicit assumptions. If something needs to happen, state it explicitly.

<!-- section_id: "20b99cfa-94ae-4dcc-a2ec-04b47f627154" -->
### 2. **Consistency Over Convenience**
It's better to be consistent across all sections than to have slightly different wording for convenience.

<!-- section_id: "fa20312b-74cd-4ff6-a6b0-1df75a087fcd" -->
### 3. **Complete Over Partial**
When defining a behavior, include all aspects: the action, the error handling, the visibility rules, and the waiting logic.

<!-- section_id: "3bd4049c-7420-4de7-adb1-7d5506c70eed" -->
### 4. **Separate Concerns**
- Internal operations: Hidden
- User-facing operations: Visible
- State management: Separate persona
- Developer tools: Separate persona, completely silent

<!-- section_id: "bd72ac42-8412-4c86-af7c-85f93ad13d78" -->
### 5. **Plan for Edge Cases**
Consider: What if file is missing? What if validation fails? What if state is null? What if user provides invalid input?

<!-- section_id: "36526c79-e633-47a0-96a2-27a869231f91" -->
### 6. **Use Strong Language for Critical Rules**
Use CRITICAL or ABSOLUTE REQUIREMENT tags for rules that must not be violated.

<!-- section_id: "89e0eb9e-bcf6-4265-854c-c6e81e7193b5" -->
### 7. **Reference External Concepts**
When referencing external concepts, include the full reference pattern: `ex:ConceptName (see filename.jsonld - read complete definition and execute all steps)`

---

<!-- section_id: "6468a6d3-6c9d-4775-9c60-fa9ee8a97aa0" -->
## Common Pitfalls to Avoid

Using the GAB tool helps you avoid these problems.

1. **Assuming behavior is obvious** - If it's not explicitly stated, it may not happen
2. **Updating one section but not others** - Similar sections need similar updates
3. **Using vague terms** - "Reasonable" and "appropriate" need to be specific
4. **Forgetting error handling** - Every file operation and validation needs error handling
5. **Mixing internal and user-facing** - Be explicit about what's visible and what's hidden
6. **Inconsistent namespaces** - Check namespace consistency when creating new files
7. **Missing file access lists** - When referencing external files, add them to access lists
8. **Multiple questions at once** - Always ask one question at a time
9. **Forgetting introductions** - All user interaction personas must introduce themselves
10. **Not distinguishing conversation types** - Internal negotiations vs. user conversations must be clearly separated
---

<!-- section_id: "b992d6b4-884c-4dec-ab18-3e3ca133d2a4" -->
## Table of Contents
1. [Use Self-Check Actors Effectively](#use-self-check-actors-effectively)
2. [Be Explicit, Not Implicit](#be-explicit-not-implicit)
3. [Manage References Systematically](#manage-references-systematically)
4. [Separate Internal from User-Facing](#separate-internal-from-user-facing)
5. [Handle Errors Proactively](#handle-errors-proactively)
6. [Design Communication Patterns](#design-communication-patterns)
7. [Plan Initialization Carefully](#plan-initialization-carefully)
8. [Use Developer Tools Correctly](#use-developer-tools-correctly)
9. [Pre-Deployment Checklist](#pre-deployment-checklist)

---

<!-- section_id: "a53452bd-e285-48ad-89b9-b5d4b6e05de0" -->
## Use Self-Check Actors Effectively

**Why this matters**: Self-check actors are GAB's built-in quality assurance mechanism. They analyze your agent definitions for vagueness, logic errors, missing instructions, and inconsistencies that would otherwise require multiple modification cycles to discover. Running self-checks systematically catches issues during development rather than after deployment, when they're harder to fix and have already affected users.

**What happens when you follow these practices**: Issues are caught early when they're easier to fix. Self-checks identify patterns of problems (e.g., "all similar personas are missing the same instruction") that you can fix systematically. You develop confidence that your agent is well-structured before deploying. The self-check process becomes part of your development workflow, preventing issues from accumulating.

**What happens when you don't**: Issues accumulate over multiple changes without detection. You discover problems only after deployment when users encounter bugs. Fixing issues becomes reactive rather than proactive, requiring emergency modifications. Similar problems appear in multiple places because you didn't systematically check for patterns. You spend more time debugging than developing.

<!-- section_id: "6655e889-62a7-4534-af41-3e7ced89fad9" -->
### 1. **Run Self-Checks After Significant Changes**
**Action**: Run `self-check actors` command after any significant modification to your agent definition.

**How to do it**:
- Run self-check after adding new actors or personas
- Run self-check after modifying responsibilities or constraints
- Run self-check after adding new protocols or file references
- Run self-check before finalizing your agent for deployment
- Make self-check part of your regular development cycle

**When to run**:
- After adding a new actor or persona
- After modifying ExecutionInstructions, Mode constraints, or Persona responsibilities
- After adding or modifying protocols
- After adding new file references
- Before deployment or major releases
- When you notice unexpected behavior (self-check may reveal the cause)

<!-- section_id: "53721dc8-e27d-40e3-a8d5-7ada9ddbe6f7" -->
### 2. **Review Self-Check Results Comprehensively**
**Action**: Don't just skim self-check reports—analyze them systematically for patterns and root causes.

**How to do it**:
- Read the full report from each actor, not just the summary
- Look for patterns: if one persona has an issue, similar personas likely have it too
- Pay attention to severity ratings (HIGH, MEDIUM, LOW) but don't ignore LOW severity issues
- Check if issues are related (e.g., missing file access often correlates with missing aalangKnowledge)
- Review proposed fixes—they often reveal the underlying problem

**What to look for**:
- **Patterns across actors**: If LearningPersona1 has a missing instruction, check if LearningPersona2 has it too
- **Cascading issues**: A missing protocol reference may cause multiple downstream problems
- **Root causes**: Multiple "missing instruction" issues may indicate a need for a shared protocol
- **Consistency problems**: Inconsistent message recipients or file access lists across similar personas

<!-- section_id: "2235f253-9356-4c05-a148-c4b3feadc7f0" -->
### 3. **Address Issues Systematically, Not Individually**
**Action**: When self-check finds multiple related issues, fix them as a group rather than one at a time.

**How to do it**:
- If similar personas have the same issue, fix all of them at once
- If multiple issues stem from the same root cause (e.g., missing protocol), fix the root cause first
- Group related fixes together (e.g., all file access issues, all visibility issues)
- After fixing, run self-check again to verify the fixes resolved the issues

**Example**:
```jsonld
// If self-check finds:
// - LearningPersona1: Missing "CRITICAL: Hide validation messages"
// - LearningPersona2: Missing "CRITICAL: Hide validation messages"
// - LearningStatePersona: Missing "CRITICAL: Hide validation process"

// Fix all three at once, then run self-check again to verify
```

<!-- section_id: "4e195208-3503-4546-940b-08c3771025a3" -->
### 4. **Use Self-Check to Verify Consistency**
**Action**: Self-check actors can identify inconsistencies that are hard to spot manually.

**How to do it**:
- Self-check will identify contradictory instructions between sections
- Self-check will find when similar personas have different instructions
- Self-check will detect when protocol references don't match actual protocol definitions
- Self-check will catch when file references aren't in access lists

**What self-check finds**:
- Contradictory instructions (e.g., ExecutionInstructions vs. Mode constraints)
- Inconsistent message recipients across similar personas
- Missing protocol implementations
- File references without corresponding access list entries
- Namespace mismatches between files

<!-- section_id: "f76afc4a-e646-4339-847f-a1d3aae4dbc2" -->
### 5. **Don't Auto-Fix—Review and Decide**
**Action**: Self-check reports issues but doesn't automatically fix them. Review each issue and decide the best fix.

**How to do it**:
- Read each issue and understand why it's a problem
- Consider the proposed fix, but evaluate if it's the best solution
- Some issues may be intentional—verify before changing
- Fix issues in order of severity, but also consider dependencies (fix root causes first)
- After fixing, run self-check again to ensure fixes didn't introduce new issues

**Decision process**:
1. Understand the issue (what's wrong and why it matters)
2. Evaluate the proposed fix (is it the best solution?)
3. Consider alternatives (could this be fixed differently?)
4. Check for dependencies (does this fix depend on other fixes?)
5. Implement the fix
6. Verify with another self-check

<!-- section_id: "869efbf4-367e-484b-8d97-21bc7939bf21" -->
### 6. **Log Self-Check Results for Tracking**
**Action**: Log self-check results to your build log to track issues over time and verify they're resolved.

**How to do it**:
- When GAB prompts to log self-check results, say yes
- Review the log entry to ensure it captures the key issues
- Use the log to track which issues have been fixed
- Reference previous self-check logs when similar issues appear

**Benefits**:
- Track issue resolution over time
- Identify recurring problem patterns
- Verify that fixes actually resolved issues
- Maintain a history of agent quality improvements

---

<!-- section_id: "4add3610-2602-4fe5-8f26-c583ee9e5763" -->
## Be Explicit, Not Implicit

**Why this matters**: LLMs interpret instructions based on their training data and context. Vague terms like "reasonable" or "appropriate" can be interpreted differently each time, leading to inconsistent behavior. Implicit assumptions about how state checks work or what happens when files are missing often result in the agent doing something unexpected or crashing when edge cases occur.

**What happens when you follow these practices**: The agent has clear, unambiguous instructions for every scenario. There's no room for interpretation, so behavior is consistent and predictable. Error conditions are handled gracefully with user-friendly messages. When you review your agent definition later, you can immediately understand what each instruction does without having to infer the behavior.

**What happens when you don't**: The agent may interpret vague instructions differently in different contexts, leading to unpredictable behavior. Missing error handling causes undefined behavior when files are missing or validation fails. Implicit state checks may not work as expected, causing the agent to proceed when it should wait or wait when it should proceed. These issues often require multiple iterations to identify and fix because the root cause (vague or missing instructions) isn't obvious.

<!-- section_id: "f5b6d853-7f6d-4719-a321-ff4d6fe6927f" -->
### 4. **Use Specific Values, Not Vague Terms**
**Action**: Replace all vague terms with exact specifications.

**How to do it**:
- Replace "reasonable" with exact numbers
- Replace "appropriate" with specific criteria
- Replace "some" with exact quantities

**Example**:
```jsonld
// BAD: Vague
"maintain reasonable size limit"
"use appropriate complexity"

// GOOD: Explicit
"maintain size limit of 50 interactions (remove oldest when exceeded)"
"use complexity level 'Competent' when user demonstrates Competent understanding with reference to the rubric"
```

<!-- section_id: "36748df1-7729-45d2-a4fa-7152217fea8c" -->
### 5. **Specify State Check Mechanisms**
**Action**: Don't just say "wait for X" - specify HOW to check if X is ready.

**How to do it**:
- State the exact message protocol to use
- Specify the state field to check
- Include the waiting condition explicitly

**Example**:
```jsonld
// BAD: Implicit
"Wait for student name"

// GOOD: Explicit
"Send state request message to ex:LearningStatePersona: 'State request: What is the current studentName value?'. If studentName is null or empty, you MUST wait. Only after receiving a valid name response, validating it, and storing it via state update message should you proceed."
```

<!-- section_id: "bfbb88fc-5aa1-48e1-9f43-170c2b217061" -->
### 6. **Document Error Handling Upfront**
**Action**: Include error handling in your initial design, not as an afterthought.

**How to do it**:
- For every file operation, specify what happens if the file is missing
- For every validation, specify what happens if validation fails
- For every state operation, specify what happens if state is null

**Example**:
```jsonld
// GOOD: Error handling included
"Read competencies.jsonld. If competencies.jsonld cannot be read (file missing or unreadable), respond with error: 'State update error: Unable to validate - competencies file not accessible'."
```

---

<!-- section_id: "fb7854a4-dafa-4a87-a172-dfd78e2eae76" -->
## Manage References Systematically

**Why this matters**: GAB agents often reference external files for concepts, principles, or data. When these references are inconsistent or incomplete, the agent can't access the information it needs, or it may access the wrong information. Namespace mismatches cause references to fail silently, and missing file access lists prevent personas from reading files they need.

**What happens when you follow these practices**: Your agent has reliable access to all external resources it needs. References work consistently because namespaces match and file access lists are complete. When you need to update a concept, you update it in one place and all references automatically use the new version. The agent's knowledge base is well-organized and maintainable.

**What happens when you don't**: References fail silently, causing the agent to behave as if concepts don't exist. The agent may try to access files that aren't in the access list, leading to errors or missing functionality. Namespace mismatches cause references between files to break, requiring you to track down and fix each reference individually. These issues are often discovered late in development when the agent fails to use expected concepts or data.

<!-- section_id: "0d0a322e-db33-48e9-8a3e-107a2aa33a31" -->
### 7. **Extract Reusable Concepts Early**
**Action**: If you find yourself repeating the same concept in multiple places, extract it to a separate file immediately.

**How to do it**:
- Create a separate JSON-LD file for the concept
- Use consistent reference pattern: `ex:ConceptName (see filename.jsonld - read complete definition and execute all steps)`
- Update all references to use the new file
- Use GAB to extract the information, put it in the new file, and add references to the new file in all locations where duplication existed.

**Example**:
```jsonld
// Create principles.jsonld with ex:AndragogyPrinciples
// Then reference it:
"Follow ex:AndragogyPrinciples (see principles.jsonld - read complete principles definition and execute all steps)"
```

<!-- section_id: "042b8643-9891-43d8-8e71-a6e22caa132d" -->
### 8. **Maintain Namespace Consistency**
**Action**: Use the same namespace across all related files.

**How to do it**:
- When creating a new file, copy the namespace from an existing related file
- Before referencing between files, verify namespaces match
- Use grep to check for namespace consistency: `grep -r "ex:" *.jsonld`

**Example**:
```jsonld
// All files should use the same namespace
File1: "ex": "https://aalang.org/example/"
File2: "ex": "https://aalang.org/example/"
File3: "ex": "https://aalang.org/example/"
```

<!-- section_id: "fc657bc7-2091-4892-86d2-080897388fd9" -->
### 9. **Complete File Access Lists**
**Action**: When you reference an external file, immediately add it to all relevant access lists.

**How to do it**:
- Add to Mode constraints file access list
- Add to each persona's aalangKnowledge
- Add to any documentation about available files

**Example**:
```jsonld
// When adding principles.jsonld:
// 1. Add to Mode constraints:
"File access: ... principles.jsonld"

// 2. Add to persona aalangKnowledge:
"aalangKnowledge": ["...", "Full access to principles.jsonld for Andragogy principles"]
```

---

<!-- section_id: "db9b83a4-aca8-4453-a58f-4df0ae77009a" -->
## Separate Internal from User-Facing

**Why this matters**: GAB agents have complex internal operations—state management, validation, persona-to-persona negotiations, file reads—that are necessary for the agent to function but should be invisible to users. When internal messages leak to users, it creates a confusing, unprofessional experience. Users see technical details like "Checking if name is valid..." or "State update: Please set currentTopic..." that they shouldn't see.

**What happens when you follow these practices**: Users see only the final results—error messages, success confirmations, and the actual conversation. The agent appears polished and professional. Internal operations happen silently in the background, and only relevant information is presented to users. Debugging is easier because you can log internal messages separately without cluttering user-facing output.

**What happens when you don't**: Users are confused by technical messages they don't understand. The agent appears buggy or unprofessional. Internal validation processes are visible, making the agent seem slow or overly technical. Persona-to-persona negotiations leak to users, breaking the illusion of a coherent conversation. These issues significantly degrade the user experience and often require multiple modification cycles to fully eliminate all internal message leaks.

<!-- section_id: "f6b467f4-a127-48b1-b54f-a9f0a49b9343" -->
### 10. **Mark All Internal Messages Explicitly**
**Action**: Every internal message type must be explicitly marked as "must NOT be shown to user". Use GAB to automate this.

**How to do it**:
- Use CRITICAL tags for visibility rules
- Mark state messages, validation processes, and internal negotiations as hidden
- Add visibility rules when you first define the message type

**Example**:
```jsonld
// When defining state messages:
"Send state request message. CRITICAL: Do NOT show this state request message to the user. It is internal only."

// When defining validation:
"CRITICAL: The validation process itself is INTERNAL and must NOT be shown to the user. Do NOT display messages like 'Checking if...', 'Validating...', 'Reading...'. Only the final validation result (error message or success) should be communicated."
```

<!-- section_id: "4bbd3a0e-c45d-468d-a0ad-7f2f9226e72c" -->
### 11. **Hide Process, Show Results**
**Action**: All process steps (reading files, comparing values, checking matches) must be silent. Only show final results.

**How to do it**:
- Use "silently" keyword for all internal operations
- Only communicate final results (errors or success)
- Explicitly prohibit process messages

**Example**:
```jsonld
// GOOD: Process hidden, result shown
"Silently read competencies.jsonld, silently extract topic names, silently compare values. If validation fails, respond with error: 'State update error: Student name cannot be a topic name.'"
```

<!-- section_id: "e98269e5-3a8e-4e21-8359-341782b45fbd" -->
### 12. **Distinguish Conversation Types**
**Action**: Explicitly define when conversations are internal (hidden) vs. user-facing (visible).

**How to do it**:
- Add clear constraints: "When communicating with the user: Create a three-way conversation"
- Add clear constraints: "When personas negotiate between themselves: These are INTERNAL discussions and must NEVER be shown to the user"
- Use distinct language for each type

**Example**:
```jsonld
// In Mode constraints:
"When communicating with the user: Create a three-way conversation (both personas + user). Both personas should participate."
"When personas negotiate between themselves: These are INTERNAL discussions and must NEVER be shown to the user."
```

---

<!-- section_id: "87046714-e7c1-417a-90fb-87168f9e36a5" -->
## Handle Errors Proactively

**Why this matters**: Real-world systems encounter errors—files may be missing, user input may be invalid, state may be null. Without error handling, these conditions cause the agent to crash, behave unpredictably, or provide cryptic error messages. Proactive error handling ensures the agent degrades gracefully and provides helpful feedback to users.

**What happens when you follow these practices**: Your agent handles edge cases gracefully. Missing files don't cause crashes—instead, the agent provides a clear error message and continues with available information. Invalid user input is caught and explained clearly. The agent is robust and reliable, even when things go wrong. Users receive helpful feedback instead of cryptic errors or crashes.

**What happens when you don't**: The agent crashes when files are missing or validation fails. Users receive confusing error messages or no feedback at all. Invalid input causes unpredictable behavior. These issues often require emergency fixes and multiple modification cycles because the root cause (missing error handling) affects many different scenarios.

<!-- section_id: "8b1d68ae-f3be-447a-a7ff-46e039192550" -->
### 13. **Plan for File Read Failures**
**Action**: Every file operation must have error handling.

**How to do it**:
- When reading a file, specify what happens if it's missing
- Provide specific, user-friendly error messages
- Continue gracefully when possible

**Example**:
```jsonld
"Read competencies.jsonld. If competencies.jsonld cannot be read (file missing or unreadable), respond with error: 'State update error: Unable to validate - competencies file not accessible'."
```

<!-- section_id: "4acf625f-e066-4002-8b96-9d5e793f28cf" -->
### 14. **Validate All User Input**
**Action**: Every user input that affects state must be validated with clear error messages.

**How to do it**:
- Specify validation rules explicitly
- Provide specific error messages for each validation failure
- Handle edge cases (null, empty, invalid format)

**Example**:
```jsonld
"Validate studentName: must be non-empty string, reasonable length (1-50 characters). If validation fails, respond with error: 'State update error: Student name must be a valid name (1-50 characters)'."
```

---

<!-- section_id: "bcffc68e-5370-4c22-a1d9-e95d543a0aa4" -->
## Design Communication Patterns

**Why this matters**: How your agent communicates with users determines the quality of the interaction. Asking multiple questions at once overwhelms users and makes it unclear what they should respond to. Not waiting for responses causes the agent to proceed before users are ready. Unclear conversation structure (internal vs. user-facing) creates confusion about who is talking to whom.

**What happens when you follow these practices**: Users have clear, focused interactions. They know what question to answer and when. The conversation flows naturally with proper pauses for user input. Multiple personas create an engaging three-way conversation without confusing internal negotiations. The agent feels responsive and attentive to user needs.

**What happens when you don't**: Users are overwhelmed by multiple questions or confused when the agent proceeds without waiting for their response. The conversation feels rushed or disjointed. Internal persona negotiations leak to users, breaking the conversation flow. These issues create a poor user experience and often require multiple modification cycles to fix because communication patterns are deeply embedded in the agent's behavior.

<!-- section_id: "615adcc6-eca7-490e-9c7e-111bfcf5fc42" -->
### 15. **One Question at a Time**
**Action**: Always ask one question and wait for response before asking another.

**How to do it**:
- Add explicit constraint: "Ask ONE question at a time and WAIT for the user's response"
- Prohibit multiple questions in a single message
- Specify the waiting mechanism

**Example**:
```jsonld
"CRITICAL: When asking questions to the user, ask ONE question at a time and WAIT for the user's response before asking another question. Do NOT ask multiple questions in a single message."
```

<!-- section_id: "d8668ad3-5159-4504-b626-635826888c20" -->
### 16. **Define Waiting Logic**
**Action**: When asking a question, specify how to wait and what to do while waiting.

**How to do it**:
- Use state flags: "set waitingForUserResponse = true when asking, false after receiving response"
- Specify what NOT to do while waiting
- Specify when to proceed

**Example**:
```jsonld
"When asking user questions: Ask ONE question at a time and WAIT for the user's response. Wait for response before proceeding (set waitingForUserResponse = true in isolated state, false after receiving response). Do NOT proceed with actions until you receive explicit user answer."
```

<!-- section_id: "20016912-954a-46d0-9de2-d0e7a69e3d7b" -->
### 17. **Plan Three-Way Conversations**
**Action**: When multiple personas interact with users, explicitly define the conversation structure.

**How to do it**:
- Specify that all personas should participate
- Clarify that this is a multi-way conversation (personas + user)
- Distinguish from internal persona-to-persona discussions

**Example**:
```jsonld
"When communicating with the user: Create a three-way conversation (both personas + user). Both personas should participate in the conversation with the user."
```

---

<!-- section_id: "3363b211-c12d-4090-9401-37d70c2fb014" -->
## Plan Initialization Carefully

**Why this matters**: The initial interaction sets the tone for the entire user experience. If personas don't introduce themselves, the user doesn't know who they're talking to. If the agent doesn't wait for required input (like a name), it proceeds with incomplete information. If the initialization sequence is unclear, different personas may duplicate or skip steps.

**What happens when you follow these practices**: Users have a clear, professional first impression. Personas introduce themselves properly, creating a welcoming experience. The agent waits for required information before proceeding, ensuring it has everything it needs. The initialization sequence is predictable and complete, with no missing or duplicated steps.

**What happens when you don't**: Users are confused about who they're talking to or what they should do first. The agent may proceed without required information, causing errors later. Steps may be duplicated (e.g., asking for name twice) or skipped (e.g., missing introductions). These issues create a poor first impression and often require multiple modification cycles to fix because initialization affects the entire conversation flow.

<!-- section_id: "a4c3947a-0824-4ece-aebd-701f74fb2188" -->
### 18. **Specify Complete Initial Response**
**Action**: Define every component of the initial response explicitly.

**How to do it**:
- Use numbered steps: "(1) X, (2) Y, (3) Z"
- Mark required vs optional clearly
- Specify who does what

**Example**:
```jsonld
"In initial response sequence: (1) BOTH personas MUST introduce themselves by name, (2) Show 'Created using AALang and Gab' attribution, (3) LearningPersona1 should present the name question..."
```

<!-- section_id: "15dd01e0-179a-4818-9c61-79641d6acdaa" -->
### 19. **Use Explicit Stop Instructions**
**Action**: When the system must wait, use strong language like "ABSOLUTE STOP" or "MUST STOP".

**How to do it**:
- Specify what to wait for
- Specify what NOT to do while waiting
- Specify when to proceed

**Example**:
```jsonld
"ABSOLUTE STOP: Wait for student's name response - do NOT show topic list, do NOT proceed with ANY actions until valid name is received and stored."
```

---

<!-- section_id: "0ccd0e1d-60e7-4342-9d10-429017b5e735" -->
## Use Developer Tools Correctly

**Why this matters**: Developer tools like debug mode are essential for development but should be completely invisible to end users. When debug mode or other developer tools are mentioned to users, it breaks the professional appearance of the agent and confuses users who don't need to know about internal development features.

**What happens when you follow these practices**: Developer tools work silently in the background, providing useful debugging information without affecting the user experience. Users never see debug messages or developer tool acknowledgments. The agent maintains a professional appearance. Development and debugging are easier because tools are available when needed but don't interfere with normal operation.

**What happens when you don't**: Users see debug messages or developer tool acknowledgments, making the agent appear unprofessional or buggy. Users may be confused by technical messages they don't understand. The developer tool functionality leaks into the user-facing experience, degrading the overall quality of the agent.

<!-- section_id: "1d3155aa-7194-4db5-a9d3-5d41a9a5cdcd" -->
### 20. **Make Developer Tools Invisible**
**Action**: Developer tools (like debug mode) must be completely invisible to end users.

**How to do it**:
- Add explicit prohibition: "NEVER mention debug mode to users"
- Hide all debug-related messages
- Make toggle commands work silently

**Example**:
```jsonld
"CRITICAL: Do NOT acknowledge debug mode toggle to user. Do NOT mention debug mode in any user-facing output. Debug mode is a silent developer tool."
```

---

<!-- section_id: "fc050a45-a4e9-4373-9eab-53ad186421e9" -->
## Pre-Deployment Checklist

Before finalizing your GAB agent, verify each item:

<!-- section_id: "9e207fd8-aa6a-4f41-a8a3-0ef0baaeef32" -->
### Consistency Checks
- [ ] Pattern count matches actual actor count everywhere
- [ ] All similar actors have consistent instructions
- [ ] No contradictory instructions between ExecutionInstructions, Mode constraints, and Persona responsibilities
- [ ] Namespaces are consistent across all related files

<!-- section_id: "ff88eb6d-de2c-4b7c-b761-f95c753bf1d5" -->
### Reference Checks
- [ ] All external files referenced are in file access lists
- [ ] All external files referenced are in persona aalangKnowledge
- [ ] All references use consistent pattern: `ex:ConceptName (see filename.jsonld - read complete definition and execute all steps)`

<!-- section_id: "262efb3a-d534-4e99-a7e3-49648f392982" -->
### Visibility Checks
- [ ] All internal messages marked as "must NOT be shown to user"
- [ ] Validation processes are hidden (only results shown)
- [ ] Internal persona-to-persona negotiations are hidden
- [ ] Three-way conversations with user are clearly defined
- [ ] Debug mode is completely silent (never mentioned to users)

<!-- section_id: "5ae069c1-5f6b-4816-9d84-be63f6ef15e3" -->
### Error Handling Checks
- [ ] File read operations have error handling
- [ ] Validation operations have error handling
- [ ] State operations handle null/empty cases
- [ ] User input validation has clear error messages

<!-- section_id: "cd3df0dc-08f3-431b-b83d-bd25a342b36d" -->
### Communication Checks
- [ ] One question at a time (not multiple)
- [ ] Waiting logic is explicit
- [ ] Both personas introduce themselves in initial response
- [ ] Three-way conversation vs internal discussions clearly distinguished

<!-- section_id: "014b7084-da26-45ff-84e5-fc7f7312fe76" -->
### Syntax and Structure Checks
- [ ] No syntax errors (run linter)
- [ ] All CRITICAL behaviors marked with CRITICAL or ABSOLUTE REQUIREMENT
- [ ] Communication permissions are correct for all actors
- [ ] All vague terms replaced with specific values


---

<!-- section_id: "a5b0bc55-05ac-4d37-8f61-c9f01ced67af" -->
## Summary

The practices in this document address the root causes of instability and repeated modification cycles in GAB agents. By following these practices from the start, you create agents that are:

- **Consistent**: All sections tell the same story, eliminating contradictory instructions
- **Explicit**: Clear, unambiguous instructions leave no room for misinterpretation
- **Robust**: Error handling ensures graceful degradation instead of crashes
- **Professional**: Internal operations stay hidden, creating a polished user experience
- **Maintainable**: Well-organized references and consistent patterns make updates straightforward

The most effective practices for creating stable GAB agents are:

1. **Be consistent** - Same instructions across all similar sections prevents unpredictable behavior
2. **Be explicit** - State everything clearly, don't assume; eliminates interpretation errors
3. **Plan for errors** - Handle file failures and validation errors prevents crashes and provides helpful feedback
4. **Separate concerns** - Internal vs. user-facing must be explicit; creates professional user experience
5. **Use specific values** - Replace vague terms with exact specifications; ensures predictable behavior
6. **Check systematically** - Use the pre-deployment checklist before finalizing; catches issues before deployment

**The bottom line**: Following these practices from the start typically reduces modification cycles from 10+ to 2-3, catches issues during development rather than after deployment, and creates agents that behave predictably and provide a professional user experience. The upfront investment in consistency, explicitness, and error handling pays off significantly in reduced debugging time and improved agent quality.
