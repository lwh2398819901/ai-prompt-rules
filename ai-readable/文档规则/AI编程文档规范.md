# AI PROGRAMMING DOCUMENTATION SPECIFICATION

You MUST follow these rules when creating or maintaining documentation for AI-assisted programming.

---

## CORE PHILOSOPHY

```
AI needs "precise context", NOT "complete knowledge base"
```

Every line in AI context MUST be relevant. Irrelevant content wastes tokens and causes confusion.

---

## SEVEN CORE PRINCIPLES

### Principle 1: INFORMATION DENSITY FIRST

**Rule**: Every line MUST be worth reading.

**MANDATORY**:
- Avoid redundancy and filler text
- Choose appropriate representation format

**Format Selection**:
| Instead of... | Use... |
|---------------|--------|
| Long paragraphs | Tables / Lists / Pseudocode / Flowcharts |
| Verbose explanations | Concise bullet points |
| Repeated information | Single source with references |

---

### Principle 2: MODULARIZATION

**Rule**: Control document length within reasonable limits.

| Document Type | Recommended Lines | Maximum Lines | Reason |
|---------------|-------------------|---------------|--------|
| Page/Module docs | 150-300 | 500 | AI context window limits |
| General spec docs | 200-400 | 800 | Need complete mapping tables |
| Deep-dive docs | 300-600 | 1000 | Complex mechanisms need detail |
| API interface docs | 50-100 per API | 200 | Complete single interface definition |

**✅ CORRECT Structure**:
```
docs/
├── modules/
│   ├── 01-认证与权限.md        (200 lines)
│   ├── 02-代理商管理.md        (300 lines)
│   └── 03-OAuth授权.md         (200 lines)
```

**❌ WRONG Structure**:
```
docs/
└── 后端实现指南.md              (3192 lines) ← AI will lose key information
```

---

### Principle 3: SINGLE RESPONSIBILITY

**Rule**: One document describes ONE module/page/feature.

**✅ CORRECT**:
- `pages/用户管理.md` - ONLY user management page
- `modules/OAuth授权.md` - ONLY OAuth authorization module

**❌ WRONG**:
- `前端实现指南.md` - Contains 9 pages (2456 lines)
- `后端实现指南.md` - Contains 8 modules (3192 lines)

---

### Principle 4: PRECISE RELEVANCE

**Rule**: Every line in AI context MUST relate to current task.

**Example**:
```
Task: Implement user login feature

✅ GOOD Context (~400 lines total):
  01-系统模型.md#权限体系 (50 lines)
  modules/01-认证与权限.md (200 lines)
  api/api-01-认证.md#登录接口 (50 lines)
  02-数据库设计.md#users表 (30 lines)

❌ BAD Context (3192 lines total):
  03-后端实现指南.md (3192 lines)
    ├─ Login logic (needed) ✅
    ├─ Agency management (NOT needed) ❌
    ├─ Log fetching (NOT needed) ❌
    └─ Export tasks (NOT needed) ❌
```

---

### Principle 5: VISUALIZATION FIRST

**Rule**: Use diagrams instead of long text descriptions.

| Content Type | Recommended Format | Use Case |
|--------------|-------------------|----------|
| Comparisons, categories, enums | Tables | Multi-dimension comparison, configs, mappings |
| Steps, points, checklists | Lists | Linear flows, summaries |
| Algorithm logic, conditionals | Pseudocode | Complex logic, algorithm steps |
| Sequences, state transitions | Flowcharts | Multi-path flows, state machines |

**Example - UI Layout (Use ASCII)**:
```
┌─────────────────────────────────┐
│ 用户管理            [新增用户]  │
├─────────────────────────────────┤
│ 表格：                          │
│ ┌────┬────┬────┬──────────┐   │
│ │ ID │姓名│角色│ 操作     │   │
│ └────┴────┴────┴──────────┘   │
└─────────────────────────────────┘
```

---

### Principle 6: COMPLETE SELF-CONTAINMENT

**Rule**: AI can work independently after reading ONE document.

**MANDATORY**:
- Include all necessary information directly
- Do NOT rely on implicit assumptions
- Third-party official docs can be linked, but core info MUST be embedded

---

### Principle 7: CROSS-REFERENCE

**Rule**: Documents reference each other via links. NEVER duplicate content.

**✅ CORRECT**:
```markdown
## 权限验证

> **详细定义**: 见 [01-系统模型.md#权限体系](../01-系统模型.md#权限体系)

**验证流程**：
- SUPER_ADMIN：直接放行
- ADMIN：直接放行
- USER：检查user_agency_binding表
```

**❌ WRONG**:
```markdown
## 权限验证

权限体系分为三层：
- SUPER_ADMIN：全局唯一，不可删除...（copy-paste 500 lines）
```

---

## DOCUMENT ARCHITECTURE

### Three-Layer Structure

```
Layer 1: FOUNDATION (Understand System)
  ├─ 00-快速导航.md              Quick index
  ├─ 01-系统模型.md              Core concepts, entity relations
  └─ 02-数据库设计.md            Data structures

Layer 2: IMPLEMENTATION (Specific Implementation)
  ├─ backend/modules/            Backend module docs (8-10)
  ├─ frontend/pages/             Frontend page docs (9)
  └─ api/                        API docs (split by module)

Layer 3: SPECIALIZED (Deep Mechanisms)
  ├─ advanced/                   Complex mechanism deep-dives
  └─ external/                   External system integration
```

### AI Usage Strategy

| Development Scenario | Layer 1 | Layer 2 | Layer 3 | Total Lines |
|---------------------|---------|---------|---------|-------------|
| Quick system overview | ✅ All | ❌ | ❌ | ~600 |
| Implement single module | ✅ Relevant parts | ✅ That module | ❌ | ~400 |
| Implement complex feature | ✅ Relevant parts | ✅ That module | ✅ Relevant specialized | ~800 |
| Fix bug | ❌ | ✅ Relevant modules | ✅ Maybe needed | ~500 |

**TARGET**: Keep context under **1000 lines**

---

## CONTENT RULES

### What to Write vs What NOT to Write

**FRONTEND Documents**:
```
Frontend doc = Product design + Interaction spec ≠ Technical implementation manual
```

| ✅ SHOULD Write | ❌ SHOULD NOT Write |
|-----------------|---------------------|
| UI layout (ASCII diagrams) | Vue component code |
| User interaction flows | State management implementation |
| Form field definitions | Form validation code |
| Which API to call | Axios wrapper logic |
| Enum value mappings | Utility function implementations |
| Button permission rules | Route guard code |

**BACKEND Documents**:
```
Backend doc = Business flow + Implementation points ≠ Complete code implementation
```

| ✅ SHOULD Write | ❌ SHOULD NOT Write |
|-----------------|---------------------|
| Business flowcharts | Complete Python code |
| Key design decisions | Utility function implementations |
| Data structure definitions | ORM query statements |
| Pseudocode logic | Exception handling details |
| API call sequences | HTTP client wrappers |

---

## WRITING RULES

| Rule | Do | Don't | Correct |
|------|-----|-------|---------|
| Avoid vague words | Be specific | ❌ "可能/通常/等等" | ✅ "5秒/每小时/立即" |
| Avoid passive voice | State who does what | ❌ "token需要被处理" | ✅ "系统处理token" |
| Avoid assumptions | State preconditions | ❌ "显然/当然" | ✅ "假设用户已登录" |
| Avoid external link dependency | Include core info | ❌ "详见文档X" | ✅ Explain in this doc |

---

## DOCUMENT MAINTENANCE

### Modification Principles

**When Issues Found**:
- ✅ Directly modify source document
- ✅ Synchronously update related documents
- ❌ NEVER add change notes
- ❌ NEVER preserve history records

### PROHIBITED Items

- ❌ Version numbers / Change logs
- ❌ "Why not XXX" (unless critical trade-off)
- ❌ "TODO" / "待办" / "后续确认"
- ❌ Design evolution history
- ❌ Excessive references (max 2-3 jumps)

### Document Linkage

**Any modification may trigger chain updates. Check related documents when modifying.**

| Change Type | In Document | Must Update | Reason |
|-------------|-------------|-------------|--------|
| Core entity/flow change | System model | Data design, Backend, Frontend, API | Business foundation changed |
| Table field add/remove | Data design | System model, Backend, Frontend, API | Data structure changed |
| API param/response change | Interface definition | Frontend, Backend, Data design | Contract changed |
| Permission/role rule change | System model | Backend, Frontend, Data design | Business logic changed |

---

## QUALITY CHECKLIST

### Single Document Check

- [ ] Line count: < 500 (module) or < 200 (page)?
- [ ] Single responsibility: Describes only ONE module/page/feature?
- [ ] Visualization: Uses diagrams instead of long text?
- [ ] Cross-reference: Avoids duplication, uses links?
- [ ] Clear goal: AI knows "what to do" after reading?

### AI-Friendliness Check

Test method: Simulate AI using documentation for a development task.

1. ✅ Can find relevant doc within 3 clicks?
2. ✅ Total relevant doc lines < 1000?
3. ✅ AI can generate correct code after reading?
4. ✅ Avoids loading irrelevant content?

---

## SUMMARY

**Golden Rules for AI Programming Documentation**:

```
1. Modularize: < 500 lines/document
2. Single Responsibility: One document = One feature
3. Precise Relevance: Only give AI what it needs
4. Visualize: Diagrams > Text
5. Frontend: Interaction flow > Technical implementation
6. Backend: Business flow > Code details
```

**Ultimate Goal**: Let AI understand requirements like a human developer, NOT search information like a search engine.

| Dimension | Requirement |
|-----------|-------------|
| Content | Specific > Abstract |
| Layout | Tables/Lists/Pseudocode/Flowcharts > Paragraphs |
| Precision | Numbers > Descriptions |
| Independence | One document = One decision unit |
| Maintenance | Direct replacement, no history |
| Readability | AI can execute independently |
