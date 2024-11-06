Aider 是 [Aider](https://aider.chat/) 辅组Ai开发的开源库，用法上类似cursor。
下面是使用流程。
首先已经由一个写好的项目库，但是我们不怎么了解这个库中的代码，无论是什么语言java,c++,python。
1.创建python venv环境
python -m venv .venv
.venv\Script\activate
2.安装 Aider
python -m pip install -U aider-chat
3.设置环境变量
参考文档[使用中转站](https://aider.chat/docs/llms/openai-compat.html)
4.设置模型
aider --model openai/o1-mini
如果是原生的openaiKey，设置的方式是aider --model o1-mini
5.设置后，aider应该启动了

[命令参考](https://aider.chat/docs/usage/commands.html)

它会很智能的实现对代码解释和优化建议，可以考虑开发一个有效的IDEA的插件，然后实现了Cursor类似的编码体验。