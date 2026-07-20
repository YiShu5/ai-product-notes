# 【C语言】解决VScode中文乱码问题

> 原文：[https://blog.csdn.net/2302_79751907/article/details/148851702](https://blog.csdn.net/2302_79751907/article/details/148851702)  
> 作者：意疏｜许可：CC BY-SA 4.0

---

## 【C语言】解决VScode中文乱码问题

---

💬欢迎交流：在学习过程中如果你有任何疑问或想法，欢迎在评论区留言，我们可以共同探讨学习的内容。你的支持是我持续创作的动力！👍点赞、收藏与推荐：如果你觉得这篇文章对你有所帮助，请不要忘记点赞、收藏，并分享给更多的小伙伴！你们的鼓励是我不断进步的源泉！🚀推广给更多人：如果你认为这篇文章对你有帮助，欢迎分享给更多对C语言感兴趣的朋友，让我们一起进步，共同提升！

作者今天格式化了电脑 想用VScode 结果会弹出乱码 故而出现了这篇文章。 代码： 如果我们想要打出最简单的代码 你好

```
#include <stdio.h>
int main()
{
 printf("你好\n");
 return 0;
}
```

会出现很奇怪的文字？ 这可不行 解决方法： VScode搜索Code Runner 就是这个插件 咱们打开这个插件下翻 找到这片代码 只复制我红框 框起来的地方（注意我这里是加入过下面东西的 你们复制插件代码就可以）

```
"code-runner.executorMap": {
 "javascript": "node",
 "php": "C:\\php\\php.exe",
 "python": "python",
 "perl": "perl",
 "ruby": "C:\\Ruby23-x64\\bin\\ruby.exe",
 "go": "go run",
 "html": "\"C:\\Program Files (x86)\\Google\\Chrome\\Application\\chrome.exe\"",
 "java": "cd $dir && javac $fileName && java $fileNameWithoutExt",
 "c": "cd $dir && gcc $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt"
 }
```

之后点击左上角这个小齿轮按钮，点击设置 找到我红框位置 点击在 settings.json 中编辑 把代码粘贴到这里 在cd的前面输入：chcp 65001 && 之后我们再运行就没有乱码啦~

### 弹出无法写入用户设置的处理方法

注意如果说vscode提示了这个错误 那么就代表你的配置文件有问题 把配置文件错误的删除就正常了

### 弹出无法在只读编辑器编辑的问题处理方法

解决方法：

1. 文件 -> 首选项 -> 设置 2. 搜索 Run In Terminal 3. 勾选 Code-runner: Run In Termina**

那么我想这就是【C语言】解决VScode中文乱码问题的全部内容了~欢迎提问

---

意气风发，漫卷疏狂学习是成长的阶梯，每一次的积累都将成为未来的助力。我希望通过持续的学习，不断汲取新知识，来改变自己的命运，并将成长的过程记录在我的博客中。如果我的博客能给您带来启发，如果您喜欢我的博客内容，请不吝点赞、评论和收藏，也欢迎您关注我的博客。 您的支持是我前行的动力。听说点赞会增加自己的运气，希望您每一天都能充满活力！愿您每一天都快乐，也欢迎您常来我的博客。我叫意疏，希望我们一起成长，共同进步。 我是意疏 下次见！
