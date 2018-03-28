<h4>error对象</h4>
<p>　　error对象是包含错误信息的对象，是javascript的原生对象。当代码解析或运行时发生错误，javascript引擎就会自动产生并抛出一个error对象的实例，然后整个程序就中断在发生错误的地方</p>
<pre>
    console.log(t);//Uncaught ReferenceError: t is not defined
</pre>
<h4>error事件</h4>
<p>　　任何没有通过try-catch处理的错误都会触发window对象的error事件</p>
<p>　　error事件可以接收三个参数：错误消息、错误所在的URL和行号。多数情况下，只有错误消息有用，因为URL只是给出了文档的位置，而行号所指的代码行既可能出自嵌入的javascript代码，也可能出自外部的文件</p>
<p>　　要指定onerror事件处理程序，可以使用DOM0级技术，也可以使用DOM2级事件的标准格式</p>
<pre>
    function myerror(_message,_url,_line) {
        alert("错误信息：" + _message
            +"\n错误的URI：" + _url
            +"\n错误的行数：" + _line
        );
        return true; //屏蔽系统的事件
    }
    //绑定错误事件 DOM0级
    window.onerror = myerror;
    //触发错误示例：
    window,onload = test;
    //DOM2级
    window.addEventListener("error",function(message,url,line){
        alert(message);
    });
</pre>
<p>　　浏览器是否显示标准的错误消息，取决于onerror的返回值。如果返回值为false，则在控制台中显示错误消息；如果返回值为true，则不显示</p>
<pre>
    //控制台显示错误消息
    window.onerror = function(message,url,line){
        alert(message);
        return false;
    }
    a;

    //控制台不显示错误消息
    window.onerror = function(message,url,line){
        alert(message);
        return true;
    }
    a;
</pre>

<h4>【类型转换错误】</h4>
<p>　　类型转换错误发生在使用某个操作符，或者使用其他可能自动转换值的数据类型的语言结构时</p>
<p>　  容易发生类型转换错误的地方是流控制语句。像if之类的语句在确定下一步操作之前，会自动把任何值转换成布尔值。尤其是if语句，如果使用不当，最容易出错</p>
<p>　　未使用过的命名变量会自动被赋予undefined值。而undefined值可以被转换成布尔值false，因此下面这个函数中的if语句实际上只适用于提供了第三个参数的情况。问题在于，并不是只有undefined才会被转换成false，也不是只有字符串值才可以转换为true。例如，假设第三个参数是数值0，那么if语句的测试就会失败，而对数值1的测试则会通过</p>
<pre>
    function concat(str1,str2,str3){
        var result = str1 + str2;
        if(str3){ //绝对不要这样
            result += str3;
        }
        return result;
    }
</pre>
<p>　　在流控制语句中使用非布尔值，是极为常见的一个错误来源。为避免此类错误，就要做到在条件比较时切实传入布尔值。实际上，执行某种形式的比较就可以达到这个目的</p>
<pre>
    function concat(str1,str2,str3){
        var result = str1 + str2;
        if(typeof str3 == 'string'){ //更合适
            result += str3;
        }
        return result;
    }
</pre>

<h4>【数据类型错误】</h4>
<p>　　javascript是松散类型的，在使用变量和函数参数之前，不会对它们进行比较以确保它们的数据类型正确。为了保证不会发生数据类型错误，只能编写适当的数据类型检测代码。在将预料之外的值传递给函数的情况下，最容易发生数据类型错误</p>
<pre>
    //不安全的函数，任何非数组值都会导致错误
    function reverseSort(values){
        if(values){
            values.sort();
            values.reverse();
        }
    }
</pre>
<p>在确切知道应该传入什么类型的情况下，最好是使用instanceof来检测其数据类型</p>
<pre>
    //安全，非数组值被忽略
    function reverseSort(values){
        if(values instanceof Array){
            values.sort();
            values.reverse();
        }
    }
</pre>

<h4>【通信错误】</h4>
<p>　　随着ajax编程的兴起，Web应用程序在其生命周期内动态加载信息或功能，已经成为一件司空见惯的事。不过，javascript与服务器之间的任何一次通信，都有可能会产生错误</p>
<p>　　最常见的问题是在将数据发送给服务器之前，没有使用encodeURIComponent()对数据进行编码</p>
<pre>
    //错误
    http://www.yourdomain.com/?redir=http://www.sometherdomain.com?a=b&c=d
    //针对'redir='后面的所有字符串调用encodeURIComponent()就可以解决这个问题
    http://www.yourdomain.com/?redir=http:%3A%2F%2Fwww.sometherdomain.com%3Fa%3Db%26c%3Dd
</pre>
