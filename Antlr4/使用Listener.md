# 使用 Listener
前言: [使用前瞻 - Listener 模式](0.使用前瞻.md#listener-模式)

在 antlr4 进行完语法分析后，会产生一棵 parse tree  
在 Listener 模式中，我们通过 antlr4 提供的用于遍历语法分析树和触发 Listener 中回调方法的树遍历器: **ParseTreeWalker 类**  

所以我们需要在自己写的主程序代码中使用包含以下内容的代码：  
``` c++
#include <iostream>

#include "antlr4-runtime.h"
#include "ArrayInitLexer.h"
#include "ArrayInitParser.h"
#include "ArrayInitBaseListener.h"

using namespace antlr4;

class MyListener: public ArrayInitBaseListener{
public:
        void enterValue(ArrayInitParser::ValueContext *ctx) override{
          std::cout << "enterValue" << std::endl;
        }
};

int main(int agrc, char* argv[]){
        std::ifstream stream(argv[1]);
        ANTLRInputStream input(stream);
        // Create antlr lexer
        ArrayInitLexer lexer(&input);
        CommonTokenStream tokens(&lexer);

        // Create antlr parser
        ArrayInitParser parser(&tokens);

        // Create parser tree and set initial rule
        tree::ParseTree *tree = parser.array();
        MyListener listener;
        tree::ParseTreeWalker::DEFAULT.walk(&listener, tree);

        return 0;
}
```

我们依次来分析一下：  
## 输入流
### ANTLRInputStream
ANTLRInputSteam 是一个 antlr 的输入流类，它定义了 antlr 程序以什么作为自己的输入。  

在上例中，input 对象以打开的文件流作为参数，即意味着从文件中读取输入进行分析  

-----------------

## 词法分析
### ArrayInitLexer
其中 `ArrayInit` 是该分析器的名称，对应文件 `ArrayInit.g4`  

ArrayInitLexer 即该项目的词法分析器，并使用 antlr 的输入流初始化该词法分析器  

### CommonTokenStream
词法分析器处理字符和把 token 传递给语法分析器，通过的就是 `CommonTokenStream` 类  

tokens 对象将所有词法分析过程中创建的 token 对象整合在一起，并放入记号流当中  

---------------

## 语法分析
### ArrayInitParser
与 ArrayInitLexer 类似，该对象初始化时以记号流作为输入，分析语法后产生语法分析树。  

该对象中的每个方法都可以对应一个树的节点(.g4 文件中的规则名)  

### tree::ParseTree
为了访问语法树，我们通过 `tree::ParseTree` 对象来保存语法分析过程中产生的树并以指定的节点作为根节点  

### MyListener
我们声明一个自己重写的 Listener 对象来遍历这棵语法树  
重写的 Listener 对象应继承于 BaseListener 对象  

倘若不重写，那么这里直接使用 ArrayInitBashListener 对象即可  

### tree::ParseTreeWalker::DEFAULT.walk
`ParseTreeWalker` 就是我们要使用的树遍历器  

当遍历器访问到某一个规则节点，如 `value` 时，就会触发 `enterValue()` 函数，直到访问完其所有的子节点之后，触发 `exitValue()` 函数  