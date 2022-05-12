rasa:开源对话机器人框架---任务型AI机器人助手。商用，稳定。一个开源的功能强大的对话机器人框架，提供端到端的，工业级别的任务型+FAQ型对话机器人的支持。
逻辑黑盒子:
用户->语音->语音识别-》自然语言理解NLU-》意图&实体(j结构化)-》对话管理DM-》自然语言生成NLG-》语音合成-》用户
意图识别，实体识别，domain识别。
DM根据上下文选择合适的动作。
DM对话管理：
自然语言生成NLG:可以简单的理解成NLU的反向过程。予以表单通顺合理。
Apache Lincese,Version2.0
rasa NLU组件配置：language:zh
pipline:一个流式的信息处理：前面的组件处理完的信息，把结果传递给下一个作为输出，将下一个的输出作为下下一个的输入。头尾详解
如组件名字是HFTransformersNLP时：transformer是一个预训练模型，他需要一个很大的模型在本地，提供至少4-50个模型，
当启动一个模型如bert时，在训练时，他会检测本地的缓存，若没有缓存则会下载模型，让在合适的地方，如公共目录，这个不需要去关心。框架通通以解决
languageModelFeaturizer是一个bert版的一个分词，languageModelFeaturizer通过模型得到文本的一些特性。
DIETClassifier是rasa研究人员自己研究的一个框架，是一个两层的transformer，他能同时做NLU和ner。这就是对NLU起作用的部分
ResponseSelector:FAQ的一个组件，他就是负责QA匹配及训练及后面请求的时候所进行处理的结构。
EntitySynonymMapper:同义词归一化
Resa Core:j基于story，用户说的话：系统action:action1,action2
Domain数据：这个系统是基于深度学习网络的，需要告诉他需要哪些输入和输出。
