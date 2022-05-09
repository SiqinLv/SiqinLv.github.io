## 基于知识库的问答 ##
>1. 将Rasa和知识库整合
>>1. 需要创建ActionQueryKnowledgeBase(来自SDK包)的自定义定义动作。包含了代码逻辑，可以处理对象和属性的查询。
>>>1. 创建知识库：使用InMemoryKnowlegeBase,需要通过Json提供知识库数据。
>>>2. NLU数据：为了让机器知道用户想要进行知识库信息的查询，需要定义一个意图来表示意图。ActionQueryKnowledgeBase可获取对象类型的列表和属性。
>>>>+ 在NLU中写入意图及书的标注信息。在domain.yam中写入映射关系。
>>3. 自定义基于知识库的动作
>>>1. 通过继承ActionQueryKnowledgeBase将知识库的实例作为参数传递给构造函数。
>>>2. 以json文件作为数据来源构建InMemoryKnowledgeBase的实例，并作为知识库的实例传递给AcionQueryKnowledgeBase的构造函数。
>>>>. 将动作加入domain配置下即可。
>>2. 工作原理
>>>1. ActionQueryKnowledgeBase既需要当前提取的实体信息，又要先前对话留下的词槽
>>>2. 对象查询：所有用户的输入都会被映射。
>>>3. 属性查询：用户的请求中会包含对象信息及感兴趣的属性。
