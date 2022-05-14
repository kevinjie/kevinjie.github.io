# webpack hash chunkhash contenthash的区别


- hash：跟项目构建相关，只要项目中有文件发生改变，则hash会更改
- chunkhash：通过文件依赖解析，构建不同的chunk，chunk中依赖文件发生改变，则chunkhash会更改
- contenthash：跟文件内容相关，文件内容发生改变，则contenthash会更改