+   #{} ${}的区别

    ${}是Properties文件中的变量占位符 可以用于标签属性值和Sql内部 属于静态文本替换

    #{}是Sql参书占位符 Mybatis会将Sql中的#{}替换成？ 在执行sql前会使用PerparedStatement的参数设置方法