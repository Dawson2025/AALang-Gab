---
resource_id: "cd2ad8b4-4cf2-4ed6-935a-ac56458ec903"
---
# AATest: AALang Testing Framework

**AATest** is a comprehensive testing framework designed specifically for AALang products. It provides a structured approach to testing AALang agents, actors, and workflows through message-based test execution.

<!-- section_id: "7470bd92-a187-4a4c-8bc9-5ff15eca3da4" -->
## Overview

AATest is an AALang-based testing tool that follows the **4-mode-13-actor** pattern, similar to GAB. It evaluates test needs, generates test files, executes tests, and reports results for AALang products.

<!-- section_id: "b9d046bd-2bce-48c4-8ee4-fe7f79a4edc6" -->
### Key Features

- **Message-Based Testing**: All tests are message-based - tests send AALang messages to actors and observe resulting messages, state changes, and behaviors
- **Three Test Types**: Supports comprehensive testing at different levels of granularity
- **Automatic Test Generation**: Analyzes products and generates appropriate test files
- **LLM-Native Execution**: Tests execute within the LLM context, leveraging AALang's execution model
- **Comprehensive Reporting**: Detailed test results with pass/fail status, execution logs, and summary statistics

<!-- section_id: "22858281-9b7c-46a4-b7fc-fd3f3de50e8a" -->
## Test Types

AATest supports three distinct test types, each designed for different levels of testing:

<!-- section_id: "93242329-0898-4d1b-ac87-e4e63b92f765" -->
### 1. MessageResponseTest
**Purpose**: Tests how individual actors respond to messages - tests individual actor responsibilities in isolation

**Use Cases**:
- Verify actor behavior when receiving specific messages
- Test actor responsibilities in isolation
- Validate actor message handling logic
- Check actor state management for individual messages

**File Pattern**: `{product-name}-message-response-tests.jsonld`

<!-- section_id: "4e3e9962-8f01-4871-957e-3dc1662d20d4" -->
### 2. MessageFlowTest
**Purpose**: Tests message flow between actors, mode transitions, and state management - tests actor interactions

**Use Cases**:
- Verify communication between actors
- Test mode transitions triggered by messages
- Validate state management across actor interactions
- Check message routing and delivery

**File Pattern**: `{product-name}-message-flow-tests.jsonld`

<!-- section_id: "f8672f74-c806-4386-a2e6-1d1e5a621d0a" -->
### 3. AgentWorkflowTest
**Purpose**: Tests complete agent workflows from user perspective - tests end-to-end workflows and full agent execution

**Use Cases**:
- Test complete user workflows
- Verify end-to-end agent behavior
- Validate full agent execution paths
- Test complex multi-actor, multi-mode scenarios

**File Pattern**: `{product-name}-agent-workflow-tests.jsonld`

<!-- section_id: "baaf53ac-938b-4a2c-9425-e4f26e8f2cc8" -->
## Test Structure

All AATest tests follow a consistent structure based on the AALang test specification:

<!-- section_id: "c22ca0cc-129a-424b-bd5e-7c77ae84ef1b" -->
### Test Metadata
- **name**: Test name identifier
- **description**: Test description explaining what messages are sent, what actor/mode/workflow is being tested, and what results are expected
- **type**: Test type classification (MessageResponseTest, MessageFlowTest, or AgentWorkflowTest)
- **priority**: Optional test priority for execution order

<!-- section_id: "22d3c5c0-64b3-441b-af0d-bebe0d2ec536" -->
### Test Inputs
- **messages**: Array of AALang messages to send during test execution
- **messageSequence**: Optional ordered sequence of messages if order matters
- **testContext**: Optional additional context (e.g., initial state, preconditions)

<!-- section_id: "082b5b0e-97df-4f67-a2c4-34c99213744a" -->
### Test Outputs (Expected Observations)
- **observedMessages**: Expected messages observed in response
- **observedStateChanges**: Expected state changes observed
- **observedBehavior**: Expected behavioral observations (actor actions, mode transitions, message acceptance/rejection)

<!-- section_id: "61fa4be4-7a55-4945-ba47-e3fcdca6ef19" -->
### Test Assertions

AATest supports a comprehensive set of assertion types, all designed to be LLM-friendly:

- **contains**: Checks if output contains specific text/pattern
- **isLike**: Semantic similarity check using LLM understanding
- **boundedDeviation**: Allows variance within user-defined bounds for non-deterministic checks
- **matchesPattern**: Pattern/regex matching
- **hasStructure**: Verifies structural elements (JSON-LD nodes, graph structure)
- **followsSequence**: Verifies actions/events occur in expected order
- **satisfiesConstraint**: Logical constraint checks
- **withinRange**: Numeric range checks
- **hasProperty**: Presence of specific properties/attributes
- **excludes**: Ensures something is not present
- **semanticEquivalence**: Semantic equivalence check
- **completeness**: All required elements present
- **consistency**: Behavior consistency across runs
- **modeTransition**: AALang-specific: mode transitions occur correctly
- **actorBehavior**: AALang-specific: actor behaves according to responsibilities
- **messageFormat**: AALang-specific: messages follow AALang message format
- **stateConsistency**: State consistency before/after operations

<!-- section_id: "64c256c6-7d41-4c67-b8f4-08614b91b11d" -->
### Test Fixtures

AATest supports test fixtures and mocks:
- **Mock Actors**: Mock actors defined in test files must have `_aamock` in their id property
- **MockManagerActor_aamock**: Manages mocks during test execution
- **Auto-Generation**: Basic mocks are auto-generated, with manual override available in test files

<!-- section_id: "e57014af-1a76-483a-996e-350d5784fb00" -->
### Parameterized Tests

AATest supports parameterized tests for testing multiple scenarios with different parameter values.

<!-- section_id: "0a7887b8-b667-4a47-a8f2-2559a47c92b8" -->
### Test Suites

Tests can be organized into suites/groups for better organization and selective execution.

<!-- section_id: "7886e5fa-af0c-4976-bb89-dc57612ee6cd" -->
## AATest Workflow

AATest operates in four modes:

<!-- section_id: "42fce69c-0df3-4098-bc4d-6f2ecb57ecce" -->
### 1. Test Need Evaluation Mode 🔍
- Analyzes target product structure
- Identifies test gaps and requirements
- Determines which test types are needed
- Prioritizes test generation

<!-- section_id: "5203fd2c-beda-49d9-9705-6f3da23df5f7" -->
### 2. Test Generation Mode 📝
- Generates test files based on product analysis
- Creates MessageResponseTest, MessageFlowTest, and AgentWorkflowTest files as needed
- Validates test specifications
- Organizes tests into appropriate files

<!-- section_id: "5e7dcb47-e7ae-4176-8852-b43bf69298d7" -->
### 3. Test Execution Mode 🚀
- Executes tests by loading products as agents
- Sends test messages and observes results
- Manages mock actors during execution
- Tracks test execution state

<!-- section_id: "8b6b7307-99da-42ed-96ee-94f0a54164a8" -->
### 4. Test Result Reporting Mode 📊
- Aggregates test results
- Generates comprehensive test reports
- Provides detailed execution logs
- Reports summary statistics

<!-- section_id: "d713106b-cb2c-47e8-99ee-be33c9fc8fe1" -->
## File Organization

Test files are organized in a `tests/` subdirectory by default (user-configurable):

```
{product-directory}/
├── {product-name}.jsonld
└── tests/
    ├── {product-name}-message-response-tests.jsonld
    ├── {product-name}-message-flow-tests.jsonld
    ├── {product-name}-agent-workflow-tests.jsonld
    └── {product-name}-test-results.md
```

<!-- section_id: "e667ad17-d2a6-4c52-82dc-ec3e26044309" -->
## Test Execution

<!-- section_id: "63a14eec-ef02-4018-be37-574e5be91500" -->
### Execution Mode
- **Sequential**: Tests run one at a time in order (by priority, then alphabetically by test name)

<!-- section_id: "53fc81a5-4843-43dc-9c1f-8883f6547b2e" -->
### Filtering
- Filter tests by test type
- Execute single tests for debugging

<!-- section_id: "9806eac4-c5e6-4157-baa0-bcab29e3c35d" -->
### Verbose Mode
Verbose mode provides detailed execution logs for debugging. To enable verbose mode, simply request it when running tests. For example:
- "Run tests in verbose mode"
- "Execute tests with verbose output"
- "Run [test name] with verbose logging"

When verbose mode is enabled, AATest includes detailed execution logs for each test step:
- **For MessageResponseTests**: Step-by-step logs with input, output, LLM reasoning, and mock interactions
- **For MessageFlowTests**: Interaction logs, transition logs, state operation logs, and mock interactions
- **For AgentWorkflowTests**: Workflow execution logs, user interaction logs, agent response logs, and mode transition logs

<!-- section_id: "9afd1ad6-5766-4c34-bbfd-9d6cee21de07" -->
### Large Test Suite Best practices

For test suites with large numbers of tests (over ~50 tests), it is recommended to execute each group of tests one at a time rather than running all tests together. This best practice applies to:

- **MessageResponseTest** groups: Execute all message-response tests together, then move to the next group
- **MessageFlowTest** groups: Execute all message-flow tests together, then move to the next group
- **AgentWorkflowTest** groups: Execute all agent-workflow tests together, then move to the next group

Executing test groups separately helps manage execution complexity, improves reliability, and makes it easier to identify and debug issues within specific test categories.

You can then ask for a testing summary if you want one that combines the results of the three testing reports.

<!-- section_id: "37c18455-2ea6-44c9-821c-12f525ef5743" -->
### Test Results
- **Location**: `tests/{product-name}-test-results.md`
- **Includes**: Pass/fail status, detailed execution logs, summary statistics
- **Output**: Both console and file output

<!-- section_id: "80e31de2-03ca-456e-b31e-64008bcfd65b" -->
## Using AATest

<!-- section_id: "2181fdc7-8095-47ba-aeb8-b564b77f9ada" -->
### Prerequisites
- An LLM that can execute JSON-LD based prompts (e.g., Claude, GPT-4)
- Access to the AATest specification files (`AATest.jsonld` and `AATest_spec.jsonld`)
- An AALang product to test

<!-- section_id: "9421278b-028a-4c62-a447-17ef1e1b6698" -->
### Getting Started

1. **Load AATest**: Add the `AATest.jsonld` and `AATest_spec.jsonld` files into your LLM environment
2. **Provide Product Path**: AATest will request the path to your AALang product file
3. **Follow the Workflow**: AATest will guide you through:
   - Test Need Evaluation → Test Generation → Test Execution → Test Result Reporting
4. **Review Results**: Check the generated test results file for detailed execution logs

<!-- section_id: "850359d2-0518-455a-a69d-8bbff52461f2" -->
### Example AATest Interaction

```
You: [Load AATest.jsonld]

AATest: "Welcome to AATest! Please provide the path to your AALang product file."

You: "my-product.jsonld"

AATest: [Test Need Evaluation Mode]
        "Analyzing my-product.jsonld...
        Found 3 actors, 2 modes, 5 personas.
        Recommended tests:
        - 5 MessageResponseTests (one per persona)
        - 3 MessageFlowTests (actor interactions)
        - 2 AgentWorkflowTests (end-to-end workflows)"
        
AATest: [Test Generation Mode]
        "Generating test files...
        Created: tests/my-product-message-response-tests.jsonld
        Created: tests/my-product-message-flow-tests.jsonld
        Created: tests/my-product-agent-workflow-tests.jsonld"
        
AATest: [Test Execution Mode]
        "Executing tests...
        MessageResponseTest: test_actor_1_basic_response... PASSED
        MessageFlowTest: test_actor_communication... PASSED
        ..."
        
You: "Run tests in verbose mode"

AATest: [Test Execution Mode]
        "Executing tests with verbose output...
        MessageResponseTest: test_actor_1_basic_response
        Step: Loading test file
        Step: Adopting actor definition
        Input: {routingGraph: {...}, payload: {...}}
        Output: {response: {...}}
        Reasoning: [LLM reasoning used]
        Mock Interactions: [...]
        ... PASSED"
        
AATest: [Test Result Reporting Mode]
        "Test execution complete!
        Results saved to: tests/my-product-test-results.md"
```

<!-- section_id: "7b636b51-41b5-4090-a688-d5078bf2f427" -->
## Key Concepts

<!-- section_id: "4ac63cd2-abc5-4fdf-a8a4-fe418fe23cf8" -->
### Message-Based Testing
All AATest tests are message-based. This means:
- **Inputs are messages**: Tests send AALang messages to actors
- **Outputs are observations**: Tests observe resulting messages, state changes, and behaviors
- **No direct code execution**: Tests work within AALang's message-passing architecture

<!-- section_id: "4fd849dd-424f-4731-92a5-c0e14826e5c1" -->
### Definition Adoption
In AALang, actors **adopt definitions** - they do not simulate them. During test execution:
- The actor **becomes** the entity under test through definition adoption
- There is no simulation layer
- The actor **IS** the entity under test during execution

<!-- section_id: "4a6f4210-9774-4752-b7b1-82bce9a7379d" -->
### Bounded Non-Determinism
AATest supports bounded non-determinism through:
- **boundedDeviation** assertions
- **consistency** assertions
- User-defined deviation bounds (e.g., semantic similarity thresholds)

<!-- section_id: "6c153255-ca8d-4d04-963d-b811d2710275" -->
## Best Practices

1. **Start with MessageResponseTests**: Test individual actor behavior before testing interactions
2. **Use MessageFlowTests for Integration**: Verify actor communication and mode transitions
3. **Use AgentWorkflowTests for End-to-End**: Test complete user workflows
4. **Leverage Semantic Assertions**: Use `isLike` and `semanticEquivalence` for LLM-friendly testing
5. **Organize Tests into Suites**: Group related tests for better organization
6. **Use Parameterized Tests**: Test multiple scenarios efficiently
7. **Review Test Results**: Check detailed logs to understand test failures

<!-- section_id: "d9377166-068d-4fdb-bf03-365e93e36b8d" -->
## Getting Consistent Test Results

AATest executes within LLM contexts, which means semantic evaluation can naturally vary between runs. To achieve more consistent and reproducible test results, follow these guidelines:

**Note**: AATest provides the framework and assertion types, but achieving consistent results requires you to configure your tests appropriately. The practices below indicate what AATest does automatically versus what requires your input.

<!-- section_id: "3a90a6b9-c81a-4b86-8597-18fac13ac1dc" -->
### Use Objective Assertions When Possible

**AATest provides**: All assertion types (`contains`, `excludes`, `isLike`, `hasProperty`, `followsSequence`, `modeTransition`, `matchesPattern`, etc.)

**Requires user input**: You must choose which assertion types to use in your test definitions. Prefer objective, measurable assertions over subjective semantic checks:

- **Replace `isLike` with `contains` or `excludes`**: When checking for specific content, use `contains` to verify exact text or patterns are present, or `excludes` to ensure unwanted content is absent
- **Replace `actorBehavior` with explicit checks**: Instead of relying on semantic evaluation of actor behavior, use specific assertions like `hasProperty`, `followsSequence`, or `modeTransition` to verify concrete behaviors
- **Use `matchesPattern` for structured validation**: When you need to verify message formats or structured data, `matchesPattern` provides more deterministic results than semantic checks

**Example of user input**:
```json
{
  "observedMessages": [{
    "assertion": "contains",
    "value": "status: success"
  }]
}
```
Instead of:
```json
{
  "observedMessages": [{
    "assertion": "isLike",
    "value": "actor responded successfully"
  }]
}
```

<!-- section_id: "df1939e6-18c2-4ac2-85e7-fa72070b7fb0" -->
### Define Explicit Pass/Fail Criteria

**AATest provides**: Test execution framework that evaluates assertions and reports results

**Requires user input**: You must write clear test descriptions and define precise expected outputs. Make your test expectations clear and measurable:

- **Document explicit criteria in test descriptions**: Clearly state what constitutes a pass or fail in the test description
- **Specify expected outputs precisely**: Define exactly what messages, state changes, or behaviors should occur
- **Include verification steps**: Add explicit verification steps for state isolation, access control, and other critical behaviors

**Example of user input**:
```json
{
  "name": "test_user_authentication",
  "description": "Test verifies that actor accepts valid credentials and rejects invalid ones. Pass criteria: (1) Valid credentials return message with 'authenticated: true', (2) Invalid credentials return message with 'authenticated: false', (3) No state changes occur for invalid credentials",
  "observedMessages": [{
    "assertion": "contains",
    "value": "authenticated: true"
  }]
}
```

<!-- section_id: "0b267ae2-b5da-4d37-91b2-1432f6945bc8" -->
### Leverage Bounded Deviation for Semantic Checks

**AATest provides**: Support for `boundedDeviation` assertion type

**Requires user input**: You must configure explicit thresholds and bounds when using semantic checks. When semantic evaluation is necessary, use bounded deviation to control variance:

- **Use `boundedDeviation` with fixed thresholds**: Set explicit similarity thresholds or deviation bounds for semantic checks
- **Document acceptable variance**: Clearly define what level of variation is acceptable in test descriptions
- **Combine with objective checks**: Use semantic checks alongside objective assertions to balance flexibility with determinism

**Example of user input**:
```json
{
  "observedMessages": [{
    "assertion": "boundedDeviation",
    "value": "user greeting message",
    "threshold": 0.85,
    "baseAssertion": "isLike"
  }]
}
```
Or with explicit bounds:
```json
{
  "observedMessages": [{
    "assertion": "boundedDeviation",
    "value": "response time",
    "min": 100,
    "max": 500,
    "unit": "milliseconds"
  }]
}
```

<!-- section_id: "a7bf4eeb-6307-45a4-a126-d7e2c643d53f" -->
### Document Test Execution Requirements

**AATest provides**: `testContext` field support and test execution framework

**Requires user input**: You must specify initial state, preconditions, and execution requirements. Help ensure consistent execution across runs:

- **Specify test context requirements**: Document any initial state, preconditions, or setup needed in `testContext`
- **Clarify execution capabilities**: Note any specific LLM capabilities or configurations required for consistent results
- **Include state isolation verification**: Add explicit checks to verify state isolation and access control when relevant

**Example of user input**:
```json
{
  "name": "test_state_isolation",
  "testContext": {
    "initialState": {
      "userCount": 0,
      "activeSessions": []
    },
    "preconditions": [
      "No existing user data",
      "Actor in 'ready' mode"
    ],
    "executionRequirements": {
      "requiresStateIsolation": true,
      "requiresAccessControl": true
    }
  },
  "observedStateChanges": [{
    "assertion": "hasProperty",
    "property": "userCount",
    "value": 1
  }]
}
```

<!-- section_id: "d219715d-e7ff-4862-b6f0-558fdb6bcfd7" -->
### Understanding the Core Issue

LLM-based semantic evaluation is inherently variable because language models interpret meaning contextually. To get deterministic results, move from subjective semantic checks to objective, measurable criteria. This doesn't mean avoiding semantic assertions entirely—rather, use them strategically with appropriate bounds and combine them with objective checks for maximum reliability.

<!-- section_id: "5370f5cc-6763-40bc-8e24-c344548414d1" -->
## Integration with GAB

AATest works seamlessly with products created by GAB:
- GAB generates AALang products
- AATest tests those products
- Together, they provide a complete development and testing workflow

<!-- section_id: "87fc1d85-6be6-476a-ba9e-9e9d29a79b81" -->
## Technical Details

For complete technical specifications, see:
- `AATest_spec.jsonld`: Complete test specification and structure definitions
- `AATest.jsonld`: AATest agent implementation and execution instructions

<!-- section_id: "b6d8b237-84cd-4311-8816-fc11b960c6c5" -->
## License

AATest is part of the AALang/GAB project. See the main [LICENSE](../LICENSE) file for license information.

---

**Ready to test your AALang products?** Load `AATest.jsonld` and provide your product file path!

