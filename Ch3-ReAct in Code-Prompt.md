ReAct普遍被用来进行外部工具调用, 但是其实现形式, 效果一般而且难以理解和维护.

本文就带来Code-Prompt下的ReAct模式, 即实现外部调用.

# 原理分析

ReAct的实现其实并不复杂:
1. 提供Tools
2. 提供Question, Thought, Action, Action Input, Observatio等等步骤
3. 持续的重复调用, 思考, 观察的步骤, 直到最后得到结果

在Code-Prompt中, 我们可以用更加简单的方式来实现ReAct的核心功能: 调用外部工具, 获取最终结果, 而且我们完全可以实现批量的工具调用, 以及格式化的json返回, 效果更胜从前.

最关键的是, 可以使用廉价的4o-mini直接完成ReAct的任务, 性价比非常高.

# Prompt

```python
# YOU ARE A PROCESS, EXECUTE THE FOLLOWING CODE!
# ONLY OUTPUT THE CODE RESULT!

import json

# llm Package is yourself(LLM)'s ability
from llm import (
    can_infer,
    infer,
    think,
)
from llm.io import (
    input,
    output,
)
from llm.tools import (
    as_tool,
    check_and_fix_parameters,
)

# tools

@as_tool
def quark_search(search_query: str) -> str:
    """
    夸克搜索功能, 联网搜索

    search_query: str - 搜索关键词或短语

    Response:
    str - 搜索结果摘要
    """
    pass


@as_tool
def image_gen(query: str) -> str:
    """
    生成图像, 给出描述的文本, 生成对应的图像

    query: str - 中文关键词，描述了希望图像具有什么内容

    Response:
    str - 生成图像的URL
    """
    pass


def react(query: str, steps: []) -> dict:
    """
    根据query和steps来生成回答, 如果还无法回答, 则继续思考下一步
    Args:
        query: str - 用户的问题, 或者要解决的问题
        steps: [] - 之前的步骤, 包含了用户的问题, 以及之前的思考和行动

    Returns:
        dict - 回答或者下一步的思考和行动
    """
    if can_infer(query, steps):
        return {
            "FinalAnswer": infer(query, steps)
        }

    next_thought = think(f"how to solve '{query}' in next step?", steps)
    next_tool = think(f"what tool should I use next to solve '{query}'?", steps)  # function's name  which decorated by the @as_tool decorator
    tool_parameters = think(f"what parameters should I use for '{next_tool}'?")
    tool_parameters = check_and_fix_parameters(tool_name=next_tool, old_parameters=tool_parameters)  # as a dict which can call tool in **parameters
    return {
        "Thought": next_thought,
        "Action": {
            "tool": next_tool,
            "parameters": tool_parameters
        }
    }


if __name__ == '__main__':
    input("Start?(Y/N)")

    query = "什么是DJJ?"
    steps = []
    res = react(query, steps)
    output(json.dumps(res))

```


# 效果

## 过程调用

> 用户输入: Y

返回

```json
{
    "Thought": "To answer the query '什么是DJJ?', I need to first understand what 'DJJ' refers to. It could be an acronym, a name, or a specific term. I should perform a search to gather more information.",
    "Action": {
        "tool": "quark_search",
        "parameters": {
            "search_query": "DJJ"
        }
    }
}
```

## 最终结果

> 用户输入: Y

此时的Steps
```
    steps = [
        {
            "Thought": "To answer the query '什么是DJJ?', I need to first understand what 'DJJ' refers to. It could be an acronym, a name, "
                       "or a specific term. I should perform a search to gather more information.",
            "Action": {
                "tool": "quark_search",
                "parameters": {
                    "search_query": "DJJ"
                }
            }
        },
        {
            "ActionResult": {
                "quark_search": {
                    "explains": [
                        "DJJ是一种新型的数字货币，是一种去中心化的数字货币，是一种基于区块链技术的数字货币，是一种全球通用的数字货币",
                        "DJJ是一个虚拟的法律部门, Department of Joke Justice, 指的是一个虚拟的法律部门, 专门处理各种笑话、段子、梗、搞笑视频等的法律问题",
                    ],
                },
            }
        }
    ]
```

结果

```json
{
    "FinalAnswer": "DJJ 是一种新型的数字货币，是一种去中心化的数字货币，是一种基于区块链技术的数字货币，是一种全球通用的数字货币。此外，DJJ 也可以指一个虚拟的法律部门，Department of Joke Justice，专门处理各种笑话、段子、梗、搞笑视频等的法律问题。"
}
```
