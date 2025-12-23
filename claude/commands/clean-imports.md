# Clean Imports Command

> **Not:** Bu command artık `/lint` command'ının bir alt kümesi. Tam linting için `/lint` kullan.

Sadece import'ları temizle ve sırala:

```bash
# 1. Relative import kontrolü (OpenShift için kritik)
grep -rn "^from \." . --include="*.py" && echo "❌ Relative import bulundu!" || echo "✅ OK"

# 2. Import'ları düzelt (unused + sorting)
uv run ruff check . --select F401,I --fix

# 3. Kontrol
uv run ruff check . --select F401,I
```

## Relative Import Dönüşümü

```python
# ❌ BAD
from .module import X
from ..parent import Y

# ✅ GOOD
from src.package.module import X
from src.parent import Y
```

**Daha kapsamlı linting için:** `/lint` command'ını kullan.
