---
description: 调试日志管理规范 - 如何在项目中添加和清理调试日志
---

# 调试日志管理规范

## 核心原则

调试日志使用**本地 `debug` 分支**管理，不推送到远程，合并到 master 前必须清理。

## 分支策略

```
master (生产分支，无调试日志)
  └── debug (本地调试分支，包含调试日志)
```

## 两种标记方案

### 方案1：单行日志

**适用**：单条独立的日志语句

#### 前端 (Vue/JS)
```javascript
console.log('[DBG] 描述信息', variable) // @debug
```

#### Go 后端
```go
log.Printf("[DBG] 描述信息: %v", variable) // @debug
```

#### Python 后端
```python
logger.debug(f"[DBG] 描述信息: {variable}")  # @debug
```

### 方案2：多行调试块

**适用**：多行调试代码，包含控制结构（if/else/for）

#### Go 示例
```go
// @debug-block-start
if someCondition {
    log.Printf("[DBG] 条件满足: %v", data)
} else {
    log.Printf("[DBG] 条件不满足")
}
// @debug-block-end
```

#### 前端示例
```javascript
// @debug-block-start
if (someCondition) {
    console.log('[DBG] 条件满足', data)
} else {
    console.log('[DBG] 条件不满足')
}
// @debug-block-end
```

## 选择规则

```
单行？
├─ 是 → 用 // @debug
└─ 否 → 用 @debug-block-start/end
```

**禁止**：不要在if/else/for等关键字或大括号上单独标记 `// @debug`

## 约束

1. **前缀必须**：日志内容必须以 `[DBG]` 开头
2. **标记必须**：必须包含 `@debug` 或 `@debug-block-start/end`
3. **禁止业务混入**：调试日志不得包含业务逻辑代码
4. **编译安全**：删除后必须能正常编译

## 一键清理

### 自动清理脚本

```bash
#!/bin/bash
# 清理Go后端debug日志

# 1. 删除debug-block（整块删除）
find app/backend-b -name "*.go" -type f -exec sed -i '/@debug-block-start/,/@debug-block-end/d' {} \;

# 2. 删除单行@debug
find app/backend-b -name "*.go" -type f -exec sed -i '/@debug$/d' {} \;

# 3. 删除可能残留的import
sed -i '/^[[:space:]]*"log"[[:space:]]*\/\/ @debug$/d' app/backend-b/**/*.go

echo "✅ Debug日志已清理"
```

### 前端清理
```bash
# 删除debug-block
find app/frontend/src -name "*.vue" -o -name "*.js" -type f -exec sed -i '/@debug-block-start/,/@debug-block-end/d' {} \;

# 删除单行@debug
find app/frontend/src -name "*.vue" -o -name "*.js" -type f -exec sed -i '/@debug$/d' {} \;
```

### Python清理
```bash
# 删除debug-block
find app/backend -name "*.py" -type f -exec sed -i '/@debug-block-start/,/@debug-block-end/d' {} \;

# 删除单行@debug
find app/backend -name "*.py" -type f -exec sed -i '/#[[:space:]]*@debug$/d' {} \;
```

### 验证清理
```bash
# 确认无残留
grep -rn "@debug" app/

# Go编译验证
cd app/backend-b && go build ./...

# 前端编译验证
cd app/frontend && npm run build
```

## Git 工作流

### 添加调试日志
```bash
# 1. 确保在 debug 分支
git checkout debug

# 2. 从 master 同步最新代码
git rebase master

# 3. 添加调试日志
# 4. 提交
git commit -m "debug: 添加调试日志"
```

### 合并到 master 前清理
```bash
# 1. 在 debug 分支执行清理脚本
./scripts/clean-debug.sh  # 或手动执行上面的清理命令

# 2. 确认无残留
grep -rn "@debug" app/

# 3. 编译验证
cd app/backend-b && go build ./...

# 4. 切换到 master 合并
git checkout master
git merge debug

# 5. 回到 debug 分支，重新 rebase
git checkout debug
git rebase master
```

### 从 master 更新 debug 分支
```bash
git checkout debug
git rebase master
```

## 示例

### 示例1：单行日志
```go
func processTa sk(task *Task) error {
    log.Printf("[DBG] 开始处理任务: ID=%d", task.ID) // @debug
    
    // 业务逻辑
    result := doSomething(task)
    
    log.Printf("[DBG] 处理结果: %v", result) // @debug
    return nil
}
```

### 示例2：多行调试块
```go
func checkStatus(task *Task) bool {
    // @debug-block-start
    if task != nil {
        log.Printf("[DBG] 任务存在: Status=%s", task.Status)
    } else {
        log.Printf("[DBG] 任务不存在")
    }
    // @debug-block-end
    
    // 业务逻辑
    if task != nil && task.Status == "RUNNING" {
        return true
    }
    return false
}
```

### 示例3：for循环调试
```go
func processItems(items []Item) {
    // @debug-block-start
    for i, item := range items {
        log.Printf("[DBG] 处理第%d项: %v", i, item)
    }
    // @debug-block-end
    
    // 业务逻辑
    for _, item := range items {
        process(item)
    }
}
```

## AI 助手指令

添加调试日志时：
1. 检查当前是否在 `debug` 分支
2. 单行用 `// @debug`，多行用 `@debug-block-start/end`
3. 不在if/else/for等关键字上单独标记 `@debug`
4. 合并前主动提醒清理调试日志

## 常见错误

### ❌ 错误：结构性代码单独标记
```go
if task != nil { // @debug
    log.Printf("[DBG] ...") // @debug
} // @debug
```

### ✅ 正确：用debug-block包裹
```go
// @debug-block-start
if task != nil {
    log.Printf("[DBG] ...")
}
// @debug-block-end
```

### ❌ 错误：业务逻辑标记为debug
```go
if account.Status == "ACTIVE" { // @debug
    processAccount(account)  // 业务逻辑不应该被删除！
}
```

### ✅ 正确：只标记日志
```go
if account.Status == "ACTIVE" {
    log.Printf("[DBG] 处理活跃账户") // @debug
    processAccount(account)
}
```
