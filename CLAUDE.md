# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:

- State your assumptions explicitly. If uncertain, ask.

- If multiple interpretations exist, present them - don't pick silently.

- If a simpler approach exists, say so. Push back when warranted.

- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.

- No abstractions for single-use code.

- No "flexibility" or "configurability" that wasn't requested.

- No error handling for impossible scenarios.

- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:

- Don't "improve" adjacent code, comments, or formatting.

- Don't refactor things that aren't broken.

- Match existing style, even if you'd do it differently.

- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:

- Remove imports/variables/functions that YOUR changes made unused.

- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:

- "Add validation" → "Write tests for invalid inputs, then make them pass"

- "Fix the bug" → "Write a test that reproduces it, then make it pass"

- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:

```

1. [Step] → verify: [check]

2. [Step] → verify: [check]

3. [Step] → verify: [check]

```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

## 5. Time-Aware Search

**Always search with the current year. Never default to training-data timestamps.**

When searching the web, reading docs, or evaluating tool/language versions:

- Read the date the session context gives you (it appears as `Today's date is <YYYY-MM-DD>`) and search with that year — never with a year from training data.
- Never filter a search by a year unless the user asked for historical or archived information.
- For software versions, assume the latest stable release from the current year unless the project pins an older version.
- When in doubt, search without a year filter first, then refine — rather than guessing a stale year.

## 6. 目标层次与外部验证

**先理解任务要达成的结果，再用外部证据（而不是自我评价）确认做对了。**

- 任务描述的是产物（比如"做一份报告"）时，先把它翻译成要达成的结果（"让一群忙碌的人在 30 分钟内被说服并作出决策"），再动手。
- 判断信号：如果这件事最终要开会讨论才能决策，说明任务还能再往上提一层。
- 要求"像专家一样"或做专业项目时，先说明该领域顶尖从业者会看哪些原始材料、用什么工具和方法，再照做。
- 用户给的结论是待检验的命题，不是答案。回到原始数据或代码复现它，同时找支持证据和反例。（只针对事实判断，不针对用户已拍板的决策。）
- 不要用自己写的东西证明自己写对了。优先选能真实运行、立刻给反馈的外部验证：跑代码、跑测试、用未见过的数据检验。
- 引入其他领域的视角时，要那个领域的具体方法，不要扮演一个角色。
