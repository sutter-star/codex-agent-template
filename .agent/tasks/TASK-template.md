# TASK-XXX

## Basic Information

### Title

填写任务名称


### Status

状态：

TODO / READY / RUNNING / BLOCKED / DONE


### Priority

HIGH / MEDIUM / LOW


---

# 1. Objective

## Goal

描述这个任务最终要实现什么。


Example:

实现 PiperX 机械臂在 LeRobot 框架中的 Robot Interface。


---

# 2. Background

说明为什么需要这个任务。


Example:

当前 LeRobot 不支持 PiperX，需要增加一个适配层。


---

# 3. Dependencies

## Depends On

依赖哪些任务：

- TASK-XXX


## Blocks

该任务完成后可以解锁：

- TASK-XXX


---

# 4. Scope

## Allowed Changes

允许修改：

- 文件：
- 模块：
- 配置：


Example:

允许：

```
src/robots/piperx/*
tests/test_piperx.py
```


## Forbidden Changes

禁止修改：

- 无关模块
- 全局架构
- 第三方源码


---

# 5. Technical Requirements

需要满足的具体要求。


Example:

1. 实现 connect()

2. 实现 get_state()

3. 返回标准 RobotState 数据结构

4. 支持异常处理


---

# 6. Input / Output


## Input

输入：

- API
- 数据
- 参数
- 外部依赖


## Output

输出：

- 文件
- API
- 数据格式
- 功能


---

# 7. Implementation Notes

记录实现约束。


Example:

- 优先使用 Adapter Pattern
- 不修改 LeRobot 原始代码
- 保持接口兼容


---

# 8. Acceptance Criteria

任务完成必须满足：


## Functional

功能：

- [ ] 条件1
- [ ] 条件2


## Testing

测试：

- [ ] 单元测试通过
- [ ] Demo运行成功


## Quality

质量：

- [ ] 无明显代码重复
- [ ] 无未处理异常


---

# 9. Verification

## Test Command

运行：

```bash
填写测试命令
```


## Expected Result

预期结果：

```
填写测试通过标准
```


---

# 10. Agent Execution Record


## Implementation Summary

完成内容：

-


## Modified Files

修改：

-


## Tests

执行：

-


结果：

PASS / FAIL


## Problems Encountered

遇到的问题：

-


## Remaining Issues

遗留：

-


---

# 11. Completion Record


## Final Status

TODO / RUNNING / DONE


## Git Commit

Commit:

```
填写commit hash
```


## Completed Date

日期：


## Reviewer

审核：

```
```