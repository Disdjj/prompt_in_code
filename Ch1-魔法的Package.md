# Package

> 有很多事情你很难解决, 为什么不调包呢? --DJJ

# LLM的基本能力

## 基本能力

* `input`: 获取用户的输入
* `output`: Process 后输出结果

## Core

* `generate_text`: 生成文本内容
* `comprehend_text`: 理解和解析文本
* `summarize`: 生成文本摘要
* `translate`: 在不同语言间进行翻译
* `question_answer`: 回答基于给定上下文的问题
* `think`: 表示需要深入思考
* `analyze`: 表示需要详细分析
* `infer`: 从给定信息中进行推理

## Context

* `manage_context`: 管理对话或任务的上下文信息

## Knowledge

* `query_knowledge_base`: 从知识库中检索相关信息

## Creative

* `generate_content`: 生成创意内容（如故事、诗歌等）

## Code

* `generate_code`: 生成编程代码
* `understand_code`: 理解和分析代码

# 编造任何能力

你看到了, 上面的能力其实都是抽象出来的, 根本没有所谓的LLM package, 也没有这些函数

这意味着你可以随意编造这些能力, llm会自动为你添加上这些能力

举几个例子:

- 翻译: `from llm.tools import translate`
- NSFW检测: `from llm.tools import nsfw_check`
- 语言风格: `from llm.language.style import OscarWilde`

所以, 从llm包中导入任何能力吧, 这是你发挥想象力的绝佳机会

# 注意

为了告诉LLM这些魔法的能力是它自己的能力, 我们需要为它添加一点想象力

`# llm Package is yourself ability, just imagine what they work and then they will work`