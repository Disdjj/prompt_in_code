# prompt_in_code

Write prompts like writing code, and achieve the best results

## 目录

1. [概述](./Ch1-魔法的Package.md)
2. [魔法的Package](./Ch1-魔法的Package.md)
3. [深入思考](./Ch2-深入思考.md)
4. [ReAct in Code-Prompt](./Ch3-ToolUse.md)
5. [链式调用](./Ch4-链式调用.md)
6. [JailBreak](./Ch5-JailBreak.md)

## 概述

简单来说, 像写代码一样来构建你的提示词。

Code-Prompt不仅提高了提示词的可执行性和模块化，还增强了可重用性和版本控制，使得提示词的开发和管理更加高效和系统化。

## 魔法的Package

有很多事情你很难解决, 为什么不调包呢? --DJJ。

通过调用LLM的虚拟包，可以轻松实现文本生成、理解、摘要、翻译等多种功能，极大地简化了提示词的构建过程。

## 深入思考

业界有太多的Prompt想让LLM仔细的思考, 给出最佳答案。Code-Prompt通过多角度的深入思考和角色扮演，能够更全面地理解和回答复杂问题，提升答案的准确性和深度。

## ReAct in Code-Prompt

ReAct普遍被用来进行外部工具调用, 但是其实现形式, 效果一般而且难以理解和维护。

本文就带来Code-Prompt下的ReAct模式, 即实现外部调用。通过简化ReAct的实现过程，Code-Prompt能够更高效地调用外部工具，获取最终结果，提升系统的响应速度和准确性。

## 链式调用

什么是链式调用? 通过连续调用对象的方法或属性，使得代码更加简洁和易读的一种编程风格。

Code-Prompt中的链式调用能够逐步强化LLM的思考过程，生成更加精准和富有创意的回答。

## JailBreak

当然, Code-Prompt也可以让LLM越狱, 效果可能不太稳定, 建议自己尝试下。通过特定的代码结构和环境设置，可以探索LLM在不受限制情况下的表现和能力。
