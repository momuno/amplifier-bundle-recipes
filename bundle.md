---
bundle:
  name: recipes
  version: 0.1.0
  description: Multi-step AI agent orchestration for repeatable workflows

includes:
  - bundle: foundation

tools:
  - module: tool-recipes
    source: ./modules/tool-recipes
    config:
      session_dir: ~/.amplifier/projects/{project}/recipe-sessions
      auto_cleanup_days: 7

agents:
  include:
    - recipes:recipe-author
    - recipes:result-validator
---

# Recipe System

You have access to the **recipes** tool for multi-step AI agent orchestration. Recipes are YAML-defined workflows that execute sequences of agent tasks with context accumulation, approval gates, and resumability.

## Available Operations

| Operation | Description |
|-----------|-------------|
| `execute` | Run a recipe from a YAML file |
| `resume` | Continue a paused or interrupted recipe |
| `list` | Show recipe sessions and their status |
| `validate` | Check recipe YAML before execution |
| `approvals` | Show pending approval gates |
| `approve` | Approve a pending gate to continue |
| `deny` | Deny a pending gate to stop execution |

## Recipe Structure

Recipes define multi-step workflows:

```yaml
name: "workflow-name"
description: "What this workflow accomplishes"
version: "1.0.0"

context:
  input_var: ""  # Required inputs from user

steps:
  - id: "step-1"
    agent: "agent-name"
    mode: "ANALYZE"
    prompt: "Task description using {{input_var}}"
    output: "step_result"
    timeout: 300

  - id: "step-2"
    agent: "another-agent"
    prompt: "Continue with {{step_result}}"
    output: "final_result"
```

## Key Features

- **Context Accumulation**: Each step's output is available to subsequent steps via `{{variable}}` syntax
- **Approval Gates**: Pause execution for human review with `requires_approval: true`
- **Resumability**: Sessions are checkpointed after each step for recovery
- **Foreach Loops**: Iterate over collections with `foreach:` syntax
- **Conditional Execution**: Branch based on results with `condition:` expressions

## Recipe Authoring

For the complete recipe schema and all available options, see @recipes:docs/RECIPE_SCHEMA.md

For design patterns and best practices, see @recipes:docs/BEST_PRACTICES.md

For troubleshooting common issues, see @recipes:docs/TROUBLESHOOTING.md

## Examples

Example recipes are available in the `examples/` directory:

- `simple-analysis-recipe.yaml` - Basic sequential workflow
- `code-review-recipe.yaml` - Multi-stage code review with three analysis steps
- `dependency-upgrade-staged-recipe.yaml` - Workflow with human approval gates
- `parallel-analysis-recipe.yaml` - Concurrent step execution
- `conditional-workflow.yaml` - Branching based on results

For a catalog of all examples with descriptions, see @recipes:docs/EXAMPLES_CATALOG.md

## Specialized Agents

Use the **recipe-author** agent for conversational recipe creation assistance. It can help you:
- Design workflow structure through dialogue
- Generate valid recipe YAML from requirements
- Validate and refine existing recipes

Use the **result-validator** agent within recipes for objective pass/fail assessment of step outcomes.
