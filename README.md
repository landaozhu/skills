# 业务开发常见的skills和rules
## rules规则（强约束）
- common：公共部分，包含前端、node开发等
- umi：umi项目
- egg: egg项目
## skills
>技能，给agent的说明书
- commit-pre-check（review代码，给出错误报告）
- deal-with-code-to-fontend-logic（把代码梳理成中文逻辑，帮助开发者更快理解逻辑）
- debug-console-only(调试代码，人工执行并贴给agent报错信息，直到找到bug，最后删除调试代码)
- generate-business-docs-from-code（业务梳理，让你快速了解所做需求的业务）
- review-commit-push（提交代码，提交前通过commit-pre-check检查，没问题提交）
- find-component-entry（通过.vue/.jsx文件，找到页面入口，在梳理大范围改动的时候特别有用）