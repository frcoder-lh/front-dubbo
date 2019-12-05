# front-dubbo
前后端调用框架

dubbo框架解决了java程序之间远程调用的问题，我们还需要一个框架解决前后端调用的问题。
最简单的设想就是通过java controller层的代码生成js api层的代码。

所以，front-dubbo设计如下：

+ 后端程序通过`***/front-dubbo/api.js`接口，生成js的api层代码。
+ 前端程序通过引入`***/front-dubbo/api.js`作为js文件，就可以直接使用了。

特点：

1. 一次引入，无需修改（不需要随着后端接口的修改而调整api层）
2. api层的代码结构与controller保持一致
