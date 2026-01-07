# 示例：三文件模式如何落地

## 示例 1：调研任务

**用户需求：**“调研晨练的好处，并写一份总结”

### 循环 1：创建计划
```bash
Write task_plan.md
```

```markdown
# 任务计划：晨练益处调研

## 目标
产出一份关于晨练益处的调研总结。

## 阶段
- [ ] 阶段 1：创建本计划 ✓
- [ ] 阶段 2：搜索并收集来源
- [ ] 阶段 3：综合整理发现
- [ ] 阶段 4：交付总结

## 关键问题
1. 对身体健康有哪些好处？
2. 对心理健康有哪些好处？
3. 有哪些科学研究支持？

## 状态
**当前处于阶段 1** —— 创建计划
```

### 循环 2：调研
```bash
Read task_plan.md           # 刷新目标
WebSearch "morning exercise benefits"
Write notes.md              # 存放发现
Edit task_plan.md           # 标记阶段 2 完成
```

### 循环 3：综合整理
```bash
Read task_plan.md           # 刷新目标
Read notes.md               # 获取发现
Write morning_exercise_summary.md
Edit task_plan.md           # 标记阶段 3 完成
```

### 循环 4：交付
```bash
Read task_plan.md           # 确认完成
Deliver morning_exercise_summary.md
```

---

## 示例 2：修 Bug 任务

**用户需求：**“修复认证模块中的登录 bug”

### task_plan.md
```markdown
# 任务计划：修复登录 Bug

## 目标
定位并修复导致无法成功登录的问题。

## 阶段
- [x] 阶段 1：理解 bug 报告 ✓
- [x] 阶段 2：定位相关代码 ✓
- [ ] 阶段 3：找出根因（当前）
- [ ] 阶段 4：实现修复
- [ ] 阶段 5：测试与验证

## 关键问题
1. 报错信息是什么？
2. 哪个文件处理认证？
3. 最近有哪些变更？

## 已做决策
- 认证处理逻辑在 `src/auth/login.ts`
- 错误发生在 `validateToken()` 函数

## 遇到的错误
- [初次] TypeError: Cannot read property 'token' of undefined
  → 根因：`user` 对象没有正确 `await`

## 状态
**当前处于阶段 3** —— 已找到根因，准备修复
```

---

## 示例 3：功能开发

**用户需求：**“在设置页添加深色模式开关”

### 三文件模式如何配合

**task_plan.md:**
```markdown
# 任务计划：深色模式开关

## 目标
在设置页添加可用的深色模式开关。

## 阶段
- [x] 阶段 1：调研现有主题系统 ✓
- [x] 阶段 2：设计实现方案 ✓
- [ ] 阶段 3：实现开关组件（当前）
- [ ] 阶段 4：加入主题切换逻辑
- [ ] 阶段 5：测试与打磨

## 已做决策
- 使用 CSS 自定义属性实现主题
- 使用 `localStorage` 存储偏好
- 开关组件放在 `SettingsPage.tsx`

## 状态
**当前处于阶段 3** —— 正在构建开关组件
```

**notes.md:**
```markdown
# 笔记：深色模式实现

## 现有主题系统
- 位置：`src/styles/theme.ts`
- 方式：CSS 自定义属性
- 当前主题：仅 light

## 需要修改的文件
1. `src/styles/theme.ts` —— 添加 dark 主题配色
2. `src/components/SettingsPage.tsx` —— 添加开关
3. `src/hooks/useTheme.ts` —— 新建 hook
4. `src/App.tsx` —— 用 ThemeProvider 包裹

## 配色决策
- 深色背景：`#1a1a2e`
- 深色卡片：`#16213e`
- 深色文字：`#eaeaea`
```

**dark_mode_implementation.md：**（交付物）
```markdown
# 深色模式实现

## 改动说明

### 1. 添加 dark 主题配色
文件：`src/styles/theme.ts`
...

### 2. 新增 useTheme hook
文件：`src/hooks/useTheme.ts`
...
```

---

## 示例 4：错误恢复模式

当某件事失败时，不要隐藏它：

### 错误示范（不推荐）
```
动作：Read config.json
错误：未找到文件
动作：Read config.json  # 静默重试
动作：Read config.json  # 再次重试
```

### 正确示范（推荐）
```
动作：Read config.json
错误：未找到文件

# 更新 task_plan.md：
## 遇到的错误
- 未找到 config.json → 将创建默认配置

动作：Write config.json（默认配置）
动作：Read config.json
成功！
```

---

## “先读再决定”模式

**重大决策前永远先读计划：**

```
[已经发生了很多次工具调用……]
[上下文越来越长……]
[最初目标可能被遗忘……]

→ Read task_plan.md          # 把目标拉回注意力窗口！
→ 做出决策                    # 目标在上下文中是“新鲜”的
```

这就是 Manus 能承受 ~50 次工具调用仍不跑偏的原因：计划文件充当“目标刷新”机制。
