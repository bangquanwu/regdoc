# JS正则

## 正则基础
### 语法
```js
/**
 * 正则构造函数
 * @pattern {string|regexp} pattern - 正则表达式的文本
 * @pattern {string} [flags] - 正则表达式的匹配模式
 * @return regexp
 **/
RegExp(pattern [, flags])

new RegExp('ab+c', 'i');
new RegExp(/ab+c/, 'i');
/ab+c/i;
```
其中，flags的可选值有：
1. `g` global模式，全局匹配;找到所有匹配，而不是在第一个匹配后停止
2. `i` ignoreCase模式，忽略大小写
3. `m` multiline模式，将开始和结束字符（^和$）视为在多行上工作（也就是，分别匹配每一行的开始和结束（由 \n 或 \r 分割），而不只是只匹配整个输入字符串的最开始和最末尾处
4. `u` unicode模式; 将模式视为Unicode序列点的序列,可以正确处理四个字节的UTF-16编码，允许匹配符合Unicode某种属性的所有字符
5. `y` sticky模;粘性匹配, 仅匹配目标字符串中此正则表达式的lastIndex属性指示的索引(并且不尝试从任何后续的索引匹配)
6. `s` dotAll模式;.号匹配任何字符（包括终止符 '\n'）

### 正则表达式文本
#### 边界
||字符|匹配规则|示例|
|:-:|:-:|:-:|:-:|
|1|`^`|匹配输入的开头，如果多行（multiline）标志被设为 true，该字符也会匹配一个断行（line break）符后的开始处。|<validReg reg="^a" readOnly></validReg>|
|2|`$`|匹配输入的结尾，如果多行（multiline）标志被设为 true，该字符也会匹配一个断行（line break）符的前的结尾处。|<validReg reg="a$" readOnly></validReg>|
|3|`\b`|匹配一个零宽单词边界（zero-width word boundary），如一个字母与一个空格之间。 （不要和 [\b] 混淆）|<validReg reg="a\bc" readOnly></validReg>|
|4|`\B`|匹配一个零宽非单词边界（zero-width non-word boundary），如两个字母之间或两个空格之间|<validReg reg="a\Bc" readOnly></validReg>|



#### 字符类别
||字符|匹配规则|示例|
|:-:|:-:|:-:|:-:|
|1|`\d`|匹配一个阿拉伯数字字符0-9|<validReg reg="\d" readOnly></validReg>|
|2|`\D`|匹配一个非阿拉伯数字字符|<validReg reg="\D" readOnly></validReg>|
|3|`\w`|匹配一个基于拉丁字母中的任何字母数字，包括下划线。相当于[A-Za-z0-9_]|<validReg reg="\w" readOnly></validReg>|
|4|`\W`|匹配一个所有\w无法匹配的字符|<validReg reg="\W" readOnly></validReg>|
|5|`\t`|匹配一个水平制表符|<validReg reg="\t" readOnly></validReg>|
|6|`\v`|匹配一个垂直制表符|<validReg reg="\v" readOnly></validReg>|
|7|`\r`|匹配一个回车符|<validReg reg="\r" readOnly></validReg>|
|8|`\n`|匹配一个换行符|<validReg reg="\n" readOnly></validReg>|
|9|`\f`|匹配一个换页符|<validReg reg="\f" readOnly></validReg>|
|10|`\0`|匹配一个空白符|<validReg reg="\0" readOnly></validReg>|
|11|`\s`|匹配一个空白字符，包括空格、制表符、表单提要、行提要和其他Unicode空白字符。相当于[\f\n\r\t\u1680\u2000...]|<validReg reg="\s" readOnly></validReg>|
|12|`\S`|匹配一个非空白字符|<validReg reg="\S" readOnly></validReg>|
|13|`[\b]`|匹配一个退格符（不要与`\b`混淆）|<validReg reg="[\b]" readOnly></validReg>|
|14|`\cX`|`X`是A-Z的一个字母。匹配字符串中的一个控制字符|<validReg reg="[\cM]" readOnly></validReg>|
|15|`\xhh`|匹配编码为`hh`(两个十六进制数字)的字符|<validReg reg="\x33" readOnly></validReg>|
|16|`\uhhhh`|匹配Unicode值为`hhhh`(四个十六进制数字)的字符|<validReg reg="\x3333" readOnly></validReg>|
|17|`\u{hhhh}或者\u{hhhhh}`|匹配Unicode值为`hhhh`(四个或者五个十六进制数字)的字符|<validReg reg="\x{33333}" readOnly></validReg>|
|18|`.`|匹配除边界符和行结束符外的任意字符|<validReg reg="\x3333" readOnly></validReg>|
|19|`\`|转义符;如果后面跟随普通字符，那么这个普通字符将具有特殊含义;相反，如果后面跟随特殊字符,这个特殊字符将被转义为普通字符|<validReg reg="\d*\*" readOnly></validReg>|

#### 分组和范围
||字符|匹配规则|示例|
|:-:|:-:|:-:|:-:|
|1|`x|y`|匹配`x`或者`y`|<validReg :reg="'x\x7cy'" readOnly></validReg>|
|2|`[xyz]`|匹配xyz中的任意一个字符|<validReg reg="[xyz]" readOnly></validReg>|
|3|`[a-z]`|匹配拉丁字符a到z范围中的任意字符,注意范围符`-`只能在[a-z][A-Z][0-9]区间使用,而且顺序不能颠倒|<validReg reg="[3-6]" readOnly></validReg>|
|4|`[^xyz0-9]`|匹配除xyz三个字符外的任何字符|<validReg reg="[^xyz0-9]" readOnly></validReg>|
|5|`(x)`|捕获组;匹配x并将其记在匹配结果中,一个正则表达式可以有多个捕获组，每个捕获组都根据其在表达式中出现的先后顺序对应一个序号，后面可以根据序号引用对应捕获组匹配的内容|<validReg reg="z(x)y" readOnly showInfo></validReg>|
|6|`\n`|匹配第n个捕获组匹配到的内容|<validReg reg="z(x)y\1" readOnly showInfo></validReg>|
|7|`(?:x)`|非捕获组;匹配x但不记入匹配结果|<validReg reg="z(?:x)y" readOnly showInfo></validReg>|
|8|`(?<name>x)`|命名捕获组;匹配x并将其记在匹配结果返回的`groups`属性内`<name>`指定的名称下|<validReg reg="city=(?<city>.+)" readOnly showInfo></validReg>|

#### 数量词
||字符|匹配规则|示例|
|:-:|:-:|:-:|:-:|
|1|`x*`|匹配`x`0或多次|<validReg :reg="'x*'" readOnly></validReg>|
|2|`x+`|匹配`x`1或多次。等价于`x{1,}`|<validReg :reg="'x*'" readOnly></validReg>|
|3|`x?`|匹配`x`0或1次，如果在数量词`*`、`+`、`?`或`{}`，任意一个后面紧跟该符号(`?`),会使数量词变为非贪婪匹配，即匹配次数最小化。反之，不跟随(`?`)的量词则是贪婪匹配，即匹配次数最大化|<validReg :reg="'(xyz)?'" readOnly></validReg>|
|4|`x*?`<br/>`x+?`|像上面的`*`和`+`一样匹配前面的模式`x`，然而匹配是最小次数匹配|<validReg :reg="'x+?'" readOnly></validReg>|
|5|`x{n}`|`n`是一个正整数。匹配前面的`x`n次|<validReg :reg="'x{2}'" readOnly></validReg>|
|6|`x{n,}`|`n`是一个正整数。匹配前面的`x`至少n次|<validReg :reg="'x{2,}'" readOnly></validReg>|
|7|`x{n,m}`|`n`和`m`都是正整数。匹配前面的`x`最少n次，最多m次|<validReg :reg="'x{2,5}'" readOnly></validReg>|

#### 断言
||字符|匹配规则|示例|
|:-:|:-:|:-:|:-:|
|1|`x(?=y)`|匹配被`y`跟随的`x`|<validReg reg="jack(?=sprat)" readOnly></validReg>|
|2|`x(?!y)`|匹配不被`y`跟随的`x`|<validReg reg="\d+(?!\.)" readOnly></validReg>|
|3|`(?<=y)x`|匹配跟随`y`的`x`|<validReg reg="(?<=\$)\d+" readOnly></validReg>|
|4|`(?<!y)x`|匹配不跟随`y`的`x`|<validReg reg="(?<!\$)\d+" readOnly></validReg>|

## 正则进阶
### 正则表达式工作原理
为了有效地使用正则表达式，重要的是理解它的工作原理。下面是正则表达式处理的基本步骤
#### 第一步：编译
当你创建一个正则表达式对象时，编译器会检查你的模板有没有错误，然后将它转换成一个本机代码例程，用于执行匹配工作  
*如果你将正则表达式赋给一个变量，可以避免重复执行次步骤*
#### 第二部：设置起始位置
当一个正则表达式投入使用时，首先要确定目标字符串中开始搜索的位置。它是字符串的起始位置，或者由正则表达式的lastIndex属性指定，但是当它从第四步返回到这里的时候（因为尝试匹配失败），此位置将位于最后一次尝试起始位置推后一个字符的位置上
#### 第三步：匹配每个正则表达式的子元
正则表达式一旦找好起始位置，它将一个个地扫描目标文本和正则表达式模板。当一个特定字元匹配失败时，正则表达式将试图回溯到扫描之前的位置上，然后进入正则表达式其他可能的路径上
#### 第四步：匹配成功或失败
如果在字符串的当前位置上发现一个完全匹配，那么正则表达式宣布成功。如果正则表达式的所有可能路径都尝试过了，但是没有成功地匹配，那么正则表达式引擎回到第二部，从字符串的下一个字符重新尝试。只有字符串中的每个字符（以及最后一个字符后面的位置）都经历了这样的过程之后，还没有成功匹配，那么正则表达式就宣布彻底失败

*牢记这一过程将有助于您明智地判别那些影响正则表达式性能问题的类型。接下来我们深入剖析第三步中匹配过程的关键点：**回溯**

### 理解回溯
在大多数现代正则表达式实现中（包括js），回溯时匹配过程的基本组成部分。它很大程度上也是正则表达式强大的根源。然而，回溯计算代价昂贵，如果不够小心的话容易失控。  
因为回溯是整体性能的唯一因素，理解它的工作原理，以及如何减少使用频率，可能是编写高效正则表达式最重要的关键点。

当一个正则表达式扫描目标字符串时，它从左到右逐个匹配正则表达式的组成部分，在每个位置上测试能不能找到一个匹配。对于每一个量词和分支，都必须决定如何继续进行。如果是一个量词（诸如`*`,`+`,`?`或者`{2,}`），正则表达式必须决定何时尝试匹配更多的字符；如果遇到分支（通过|操作符），它必须从这些选项中选择一个进行尝试。

每当正则表达式需要做出选择或者决定的时候，便会产生一个决策点，它会记住这个位置，以备将来返回后使用。如果所选方案匹配成功，正则表达式将继续进行接下来的匹配，如果其余部分匹配也都成功了，那么匹配就结束了。但是如果所选择的方案未能发现响应匹配，或者后来的匹配也失败了，正则表达式将回溯到最后一个决策点,然后在剩余的选项中选择一个，继续匹配下去，直到完全匹配，或者量词和分支选项的所有可能的排列组合都尝试失败了，那么它将放弃这一过程，然后移动到此过程开始位置的下一个字符上，重复此过程。

#### 分支回溯
下面的例子演示了这一过程是如何处理分支的
```js
/h(ello|appy) hippo/.exec("hello there, happy hippo")  
```
<test-block reg="h(ello|appy) hippo" readOnly showInfo></test-block>

1. 查找h
2. 从待匹配字符串第一个字母开始匹配，h匹配成功,继续匹配
3. 出现决策点:（ello|appy），匹配第一个选项ello
4. 接着从待匹配字符串之前匹配过的位置往下匹配ello匹配成功，继续匹配
5. 空格匹配成功，继续匹配
5. h匹配t失败，返回上一个决策点->3
6. 匹配第二个选项appy
7. a匹配e失败，没有剩余决策，没有其他决策点，字符串第一个位置h开始的匹配失败
8. e匹配h失败
9. ello there, 在匹配正则的第一个字符时全部匹配失败
10. h匹配成功
11. 出现决策点:（ello|appy），匹配第一个选项ello
12. e匹配a失败，返回上一个决策点->11
13. appy hippo分别匹配成功,正则所有字符匹配结束
14. 匹配成功

#### 重复回溯
下面的例子演示带重复量词的回溯
```js
var str = `
  <p>Para 1.</p>
  <img src='smiley.jpg'>
  <p>Para 2.</p>
  <div>Div.</div>
`;
/<p>.*<\/p>/si.exec(str)
```
<test-block reg="<p>.*<\/p>" readOnly showInfo></test-block>
1. 匹配`<p>`成功
2. dotAll模式下，.*开启贪婪匹配余下所有字符`Para 1...</div>`
3. 没有剩余字符匹配`<`，匹配失败，往前回溯一个字符
4. 继续回溯，直到`</div>`
5. `d`匹配`p`失败，继续回溯，直到`<div>`
6. `d`匹配`\`失败，继续回溯，直到`</p>`
7. 匹配成功
::: tip
考虑下非贪婪匹配，或者非dotAll模式下的匹配顺序
:::

#### 回溯失控
当一个正则表达式匹配耗时达到数秒、数分钟或者更长时间，问题原因很可能是回溯失控
考虑下面这个正则表达式：
```js
/<html[^]*?
  <head[^]*?
    <title[^]*?
    <\/title>[^]*?
  <\/head>[^]*?
  <body[^]*?
  <\/body>[^]*?
<\/html>/;
```
<test-block reg="<html[^]*?<head[^]*?<title[^]*?<\/title>[^]*?<\/head>[^]*?<body[^]*?<\/body>[^]*?<\/html>" readOnly showInfo></test-block>

这个正则表达式匹配正常HTML字符串时工作良好，但是如果目标字符串缺少一个或多个标签时，就会变得十分糟糕。例如`</html>`缺失，那么最后一个[^]*将扩展到字符串的末尾，因为在那里没有发现`</html>`标签，只能回溯，然而回溯到`</body>`标签时仍然没有匹配到`</html>`字符串，然后倒数第二个`[^]*`开始回溯，然而回溯到`<body>`标签时，仍然没有匹配`</body>`标签，于是倒数第三个`[^]*`开始回溯，以此类推直到回溯到第一个量词匹配，最终以首字符开始的匹配失败, 然后重新以第二个字符开始新一轮的匹配，直到所有字符都匹配结束。
**解决回溯失控方案**

1. **减少回溯点**

在之前的匹配html文本的示例，考虑使用如下正则：
```js
/<html(?=([^]*?<head))\1
  (?=([^]*?<title))\2
  (?=([^]*?<\/title>))\3
  (?=([^]*?<\/head>))\4
  (?=([^]*?<body))\5
  (?=([^]*?<\/body>))\6
  [^]*<\/html>/
```
现在如果最后的`</html>`缺失，正则表达式将立刻失败，因为没有回溯点可以返回，断言符号只会由临时的前瞻后瞻行为不会产生回溯点
::: tip
考虑下这种减少回溯点的方法使用范围
:::

2. **快速失败**

让没有必要的回溯行为快速匹配失败，结束匹配

比如上面匹配html文本的正则，如果最后面的`</html>`缺失，如果我们在正则末尾加上$,尾部匹配限定为`</html>`,那么正则将在尾部无法匹配`</html>`时直接宣告失败，不会再回溯或者循序从字符串各个位置重新开始匹配


3. **具体化**

尽可能具体指出分隔符之间的字符具体形式。例如需要匹配script, img标签的src属性:
```js
var str = '<img src="http://a.b.c" data-src="xxx" width="xxx" height="xxx">'
// 第一种
/src="(.*)"/.exec(str);
// 第二种
/src="([^"]*)"/.exec(str);
```
第二种用更具体的`[^"]*`取代过于宽泛的`.*`,理论性能会优于第一种

4. **拆分正则**

正则表达式过于复杂，那么它的匹配性能和回溯失控的风险也会大大增加，同时其可读性也会大大降低  
拆分正则，可以将一些判断逻辑转移到代码层，降低正则复杂度，且易于维护  

## 正则实践