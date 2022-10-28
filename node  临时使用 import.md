node  临时使用 import

是谁说node不支持import等语法的，其实在node后面的版本中，已经出现了支持node import语法的提案，只是还没完全开始使用，那么，应该怎么使用呢？

     1.mjs  后缀名
    import buffer  from  'buffer'
    
    const buf=buffer.Buffer.from('nihao','ascii');
    console.log(buf.toString('hex'));
    console.log(111)
    
    node --experimental-modules 1.mjs      //注意后缀名.mjs




当你这样运行代码时，恩，你会 发现居然没有抛出上面的错误，你是否发现了重点内容：文件扩展名要为mjs和node运行时需要加–experimental-modules参数

