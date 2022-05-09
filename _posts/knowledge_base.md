## 基于知识库的问答 ##
>1. **将Rasa和知识库整合**
>>1. 需要创建ActionQueryKnowledgeBase(来自SDK包)的自定义定义动作。包含了代码逻辑，可以处理对象和属性的查询。
>>>1. 创建知识库：使用InMemoryKnowlegeBase,需要通过Json提供知识库数据。
>>>2. NLU数据：为了让机器知道用户想要进行知识库信息的查询，需要定义一个意图来表示意图。ActionQueryKnowledgeBase可获取对象类型的列表和属性。
>>>>+ 在NLU中写入意图及书的标注信息。在domain.yam中写入映射关系。
>>3. 自定义基于知识库的动作
>>>1. 通过继承ActionQueryKnowledgeBase将知识库的实例作为参数传递给构造函数。
>>>2. 以json文件作为数据来源构建InMemoryKnowledgeBase的实例，并作为知识库的实例传递给AcionQueryKnowledgeBase的构造函数。
>>>>. 将动作加入domain配置下即可。
>>2. **工作原理**
>>>1. ActionQueryKnowledgeBase既需要当前提取的实体信息，又要先前对话留下的词槽
>>>2. 对象查询：所有用户的输入都会被映射。
>>>3. 属性查询：用户的请求中会包含对象信息及感兴趣的属性。
>>>4. 解析指代：一个对象列表中的位置指代该对象的为序数指代。
>>>> 在ActionQueryKnowledgeBase中设置映射关系。
>>>> 需要将用户表达的不规则的序数映射成Last等，用NLU的实体同义词映射来完成。
>>3. **自定义ActioQueryKnowledgeBase**
>>> ***ActioQueryKnowledgeBase默认返回消息是英文***
>>>1. 当用户请求机器人返回列表是utter_objects()会被调用。utter_objects()的功能是把对象的情况给用户。
>>>>. 默认的返回结果是无法作为商用产品呈现给用户。必须基于中文的更加贴近业务的响应内容。需要用utter_obkect方式。
>>>>. 当用户请求机器人返回某一对象的具体属性时，utter_attribute_value()会被自动调用。会将查询结果返回给用户。
>>> 自定义InMemoryKnowledgeBase
>>>>- InMemoryKnowledgeBase继承KnowledgeBase类，可以通过重写ovrride类实现自定义。
>>>>- get_key_attribute_of_object():为了追踪用户最后提到的对象。存储对象的关键属性key attribute,每个对象都有一个全局的关键属性。，默认为id,可用set_key_attribute_object()来更改设置。
>>>>- 函数get_representation_function_of_object()返回一个函数对象，用于将对象映射到对象的标志。。默认为lambda obj:obj['name'],也就返回一个对象的name属性作为标志。若对象没有属性name，应调用set_representation_funciton_of_objects()来更改设置。
>>>>- set_ordinal_mention_mapping():序数指代映射用于序数指代。也可修改设置，实现自定义。
>>> 创建自定义知识库
>>>>. 在数据特别多或结构复杂的情况下，需要创建自定义知识库
>>>>>> 继承KnowledgeBase
>>>>>> 实现get_objects()，get_object()和get_attribute_of_object()方法。
