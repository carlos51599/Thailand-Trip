---
applyTo: '**'
---

# AI-Optimized Monolith Guidelines

## 🎯 Core Philosophy
This is an AI-optimized monolith. It prioritizes clarity, predictability, and navigability over traditional software engineering abstractions. Follow these patterns strictly.

---

## 🧠 Step 1: Understanding & Context Recovery

### **1. Create an `Architectural Overview` Docstring**
Include at the top of your file:
- **Responsibility:** What business problem this solves (1-2 sentences)
- **Key Interactions:** Conceptual inputs, outputs, and configuration
- **Navigation Guide:** Data flow and section markers for AI navigation
- **For Navigation:** Explicitly instruct use of VS Code outline (Ctrl+Shift+O)

**Maintainability Rule:** Document concepts that change infrequently, not implementation details.

### **2. AI Comprehension Optimization (PROVEN PATTERNS)**

**Configuration Architecture Integration**:
```python
"""
CONFIGURATION ARCHITECTURE:
- Single source of truth: All configuration in CONFIG dictionary
- Coordination boundaries: Orchestrator functions extract config values
- Primitive injection: Business logic accepts explicit typed parameters
- Zero hidden dependencies: All behavior predictable from signatures
- Full testability: Functions accept primitives, no config mocking required
"""
```

**Context Complexity Metrics**:
- **Configuration Context**: <200 lines total
- **Coordination Points**: <10 functions access CONFIG
- **CONFIG Per-Function**: <5 accesses in orchestrators, 0 in business logic
- **Hidden Dependencies**: Zero functions with undeclared dependencies
- **Type Explicitness**: 100% of parameters/returns have type hints

### **3. Fallback Search Strategy**
If you lose context:
1. Search for section markers: `# ═════`
2. Find entry point: `if __name__ == "__main__"`
3. Use AI recovery functions: `_ai_context_recovery_summary()`

---

## 🚀 Core Implementation Patterns

### **1. Structure: Single File, Clear Sections**
Use highly visible, searchable section markers:
```python
# ═══════════════════════════════════════════════════════════════════════════
# 🏗️ INITIALIZATION SECTION
# ═══════════════════════════════════════════════════════════════════════════
```

### **2. Simplicity: Prefer Data over Abstraction**
- Use **standalone functions** instead of complex class hierarchies
- Use **simple dictionaries** for data structures instead of custom classes
- Keep data shapes explicit and visible

### **3. Configuration: Hybrid Architecture Pattern (PROVEN)**

**Anti-Pattern:** Scattered global configuration dictionaries.

**Correct Pattern:** CONFIG Dictionary + Coordination Boundaries + Primitive Injection

```python
CONFIG = {
    "processing": {"batch_size": 1000},
    "validation": {"strict_mode": True}
}

# Coordination boundary - extracts CONFIG values
def orchestrator(input_data):
    batch_size = CONFIG["processing"]["batch_size"]
    strict_mode = CONFIG["validation"]["strict_mode"]
    return process_data(input_data, batch_size, strict_mode)

# Business logic - explicit parameters only
def process_data(data: Any, batch_size: int, strict_mode: bool) -> Any:
    # Function behavior completely predictable from signature
    # No hidden CONFIG dependencies
```

**Critical Rules:**
- Never create globals outside CONFIG
- Only orchestrator functions access CONFIG
- Business logic accepts primitives only
- **<10 total coordination boundary functions**
- **<5 CONFIG accesses per orchestrator function**
- **0 CONFIG accesses in business logic functions**

**Function Classification:**
- **Orchestrator**: Coordinates workflow, extracts CONFIG, calls business logic (0-5 CONFIG accesses)
- **Business Logic**: Processes data, accepts explicit parameters (0 CONFIG accesses - STRICT)

### **4. Visibility: Debugging and Modification Zones**

**Complexity Limits:**
- **Maximum nesting depth**: 4 levels (target: 3 levels)
- **Exception**: Try/except blocks don't count toward nesting

**Nesting Depth Check:**
```python
# ❌ WRONG - 5 levels
if condition_1:           # Level 1
    for item in items:    # Level 2
        if condition_2:   # Level 3
            for x in y:   # Level 4
                if c:     # Level 5 (OVER LIMIT)

# ✅ CORRECT - 3 levels (extract inner logic)
if condition_1:
    items_filtered = filter_items(items, condition_2)
    for item in items_filtered:
        process_item(item)  # Extracted function
```

**Debugging Patterns:**
- **Use logger.info() over print()** with progress indicators (🚀, 📊, ✅)
- **Structure functions with internal sections** (`# === SECTION NAME ===`)
- **Structured error messages**: `logger.error(f"❌ WORKFLOW FAILED: {str(e)}")`
- **Defensive data handling**: `df.columns = df.columns.str.strip()`
- **MODIFICATION POINT:** markers for obvious change zones
- **State summary functions**: `print_configuration()`, `_debug_current_state_for_ai()`

### **5. Testing: Simple Functions**
Write simple test functions in `tests` folder with assert statements and success indicators.

### **6. Size Constraints (STRICT - ENFORCED DURING DEVELOPMENT)**

**HARD LIMITS (Non-Negotiable):**
- **Function Maximum**: 75 lines
- **CONFIG Dictionary**: <200 lines total
- **Nesting Depth**: ≤4 levels (optimize for 3)

**Function Size Enforcement:**
Check function length at these milestones during development:
- **50 lines** → ⚠️ Warning: Approaching limit. Plan extraction strategy.
- **75 lines** → 🔴 STOP: Refactor before adding more code.
- **100 lines** → ❌ CRITICAL: Immediate refactor required.

**Why 75 Lines:**
1. AI comprehends entire function in single pass
2. Fits on single screen without scrolling
3. Enforces Single Responsibility Principle
4. Simplifies unit testing and debugging
5. Evidence: Functions >100 lines had 8× higher bug density

**Quick Refactoring Checklist:**
- Internal `# === SECTIONS ===` present? → Extract each to function
- Nested loops/conditionals? → Extract to named helpers
- Multiple responsibilities? → Split orchestration from business logic
- Repeated patterns? → Extract shared logic

**Exemption Process:** None. All functions must comply.

### **7. Type Safety Requirements (MANDATORY)**

**Rule:** All functions MUST have complete type hints on parameters and return values.

**Enforcement Checklist:**
- ✅ Every parameter has type annotation
- ✅ Return type declared (use `-> None` if no return)
- ✅ Use `Optional[T]` for nullable parameters/returns
- ✅ Import types: `from typing import List, Dict, Optional, Any`

**Example:**
```python
from typing import Optional, Dict, Any
import pandas as pd

# ❌ WRONG - No type hints
def process_data(df, config, mode=None):
    return transformed_df

# ✅ CORRECT - Complete type contract
def process_data(
    df: pd.DataFrame,
    config: Dict[str, Any],
    mode: Optional[str] = None
) -> pd.DataFrame:
    return transformed_df
```

**Why 100% Coverage:**
- AI understands function contracts without reading implementation
- Autocomplete works correctly
- Type errors caught before runtime
- Function signatures are self-documenting

**Exemptions:** None. Even single-line helpers must have type hints.

### **8. Code Duplication Prevention**

**Rule:** Shared logic MUST be extracted before duplication exceeds 20 lines.

**Detection Pattern:**
If you write similar code in two places, ask:
1. Is core logic identical? → Extract to shared function
2. Only rendering differs? → Separate data prep from rendering
3. Different APIs, same workflow? → Create data layer + multiple renderers

**Refactoring Trigger:** `Similarity > 70% AND Length > 20 lines`

**Pattern: Shared Data Layer**
```python
# ❌ WRONG - Duplicate 300-line functions
def generate_plot_matplotlib(...):
    # 250 lines of data prep (DUPLICATED)
    # 50 lines matplotlib rendering

def generate_plot_plotly(...):
    # 250 lines of data prep (DUPLICATED)
    # 50 lines plotly rendering

# ✅ CORRECT - Separated data from rendering
def prepare_plot_data(...) -> Dict[str, Any]:
    # 250 lines of data prep (SHARED)
    return {"x": x_data, "y": y_data, ...}

def render_matplotlib(plot_data: Dict[str, Any]) -> None:
    # 50 lines matplotlib rendering

def render_plotly(plot_data: Dict[str, Any]) -> None:
    # 50 lines plotly rendering
```

**Benefit:** Bug fixes in shared logic require single edit, not N edits.