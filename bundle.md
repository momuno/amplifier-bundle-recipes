---
bundle:
  name: recipes
  version: 1.0.0
  description: Multi-step AI agent orchestration for repeatable workflows

includes:
  - bundle: git+https://github.com/microsoft/amplifier-foundation@main
  - bundle: recipes:behaviors/recipes
---

# Recipe System

@recipes:context/recipe-instructions.md

---

## Creating Recipes

To create, validate, or improve recipes, **delegate to the `recipes:recipe-author` agent**. This expert will:
- Ask clarifying questions to understand your workflow
- Design the appropriate recipe structure
- Apply best practices and patterns
- Validate the result

## Examples

Example recipes are available in `@recipes:examples/`:

- `simple-analysis-recipe.yaml` - Basic sequential workflow
- `code-review-recipe.yaml` - Multi-stage review with conditional execution
- `dependency-upgrade-staged-recipe.yaml` - Workflow with human approval gates

For a complete catalog, see @recipes:docs/EXAMPLES_CATALOG.md

---

@foundation:context/shared/common-system-base.md
