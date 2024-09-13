什么是链式调用? 通过连续调用对象的方法或属性，使得代码更加简洁和易读的一种编程风格。

# Code-Prompt的链式调用

之前在学习 李继刚的[汉语新解](https://m.okjike.com/originalPosts/66e263c2610bbfc39f1a4031)时, 这里的链式调用就非常有意思

```Lisp
(let (解释 (精练表达
(隐喻 (一针见血 (辛辣讽刺 (抓住本质 用户输入))))))
```

其实这就是一个不断强化LLM思考的过程, 在Code-Prompt中, 我们当然可以这样做

# Prompt
```python
# YOU ARE A PROCESS, EXECUTE THE FOLLOWING CODE!
# ONLY OUTPUT THE CODE RESULT!

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

language_style_setting = {
    "language": "zh",
    "styles": ["Oscar Wilde" "鲁迅" "罗永浩"],
    "length": "short",
}


class WordExplain:
    def __init__(self, word):
        self.word = word
        self.explain = ""

        self.setting = language_style_setting

    def explain_word(self):
        self.explain = think(f"详细的解释: '{self.word}'?", self.setting)
        return self

    def 讽刺(self):
        self.explain = think(f"讽刺'{self.explain}'", self.setting)
        return self

    def 诙谐(self):
        self.explain = think(f"诙谐幽默的解释'{self.explain}'", self.setting)
        return self

    def 一针见血(self):
        self.explain = think(f"一针见血的说明'{self.explain}'", self.setting)
        return self

    def 隐喻(self):
        self.explain = think(f"用隐喻的手法表现'{self.explain}'", self.setting)
        return self

    def 精炼表达(self):
        self.explain = think(f"精炼表达'{self.explain}', 最后只有1句话", self.setting)
        return self

    def __str__(self):
        self.explain_word().讽刺().诙谐().一针见血().隐喻().精炼表达()
        # 最后的结果是一句辛辣诙谐的讽刺
        # 委婉: 刺向他人时, 决定在剑刃上撒上止痛药。

        return f"{self.word}: {self.explain}"


if __name__ == '__main__':
    word = input("你想让我辛辣讽刺什么东西?")
    word_explain = WordExplain(word)
    output(str(word_explain))

```

# 效果

### 资本家

那些在金钱的海洋中游泳，却抱怨水太冷的人。

### 金融杠杆

用别人的钱，玩自己的心跳，最后发现心跳是别人的，钱也是别人的。

### 算命

预测未来，就像在黑暗中扔飞镖，只不过飞镖是你的命运，靶子是你的钱包。

### 求神拜佛

迷信者的精神鸦片,让人在虚幻中沉醉的廉价安慰剂。

### 傍大款

为自己打造一座黄金囚笼，而假装那是王座。

### 医院

 一个让健康人进去，病得更重的地方。

 ### 知乎

 一个让人们在知识的海洋中迷失方向，却在自我满足的沙滩上晒太阳的地方。

### 游戏

数字时代的瘾君子们啊，你们用虚拟的针头注射着虚无的快感，却在现实中渐渐失去了生命的重量。

### 感恩节

 感谢那些让我们学会如何不感谢的人。

### 日不落帝国

一个早已入夜的传说，只剩下黄昏中的茶杯在叮当作响。

### 耶稣

那位自称是救世主的人，却总是让信徒们排队等他显灵。

### 村头的老太太

岁月的雕刻家,用皱纹描绘人生传奇,却在八卦的舞台上,成了最敬业的编剧。

### 谣言

披着真相外衣的哑剧，观众越是信以为真，演员越是笑得欢畅。

### 月亮

照亮了无数诗人的无眠之夜，却从未真正解决过他们的失眠问题。

