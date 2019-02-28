`vua` 使用typescript开发， 具有非常详尽的类型说明


`vua`中， 使用原生webpack来生成ts类型声明文件(webpack配置：scripts/webpack.config.types.js)，类型声明文件在/types下


*在.vua文件中请谨慎使用@，类型生成中不会翻译该符号，导致路径找不到的问题*