# 网页存储  Web Storage

当我们在制作网页时会希望记录一些信息，例如用户登陆状态，计数或者小游戏等，但是又不希望用到数据库，就是可以利用Web Stroage 技术将数据存储在用户浏览器中。

认识Web Stroage

> Web Storage 是一种将少量的数据存储在客户端（Client） 磁盘的技术。只能支持在WebStorage API 规格的浏览器中，网页设计者都可以使用JavaScript来操作它，我们先了解一下Web Storage.

Web Storage 提供两种方式将数据保存在客户端：一种是localStorage,另一种是sessionStroage,两者的主要差异在于生命周期有效范围

| web Storage 类型 | 生命周期       | 有效范围 |
| ---------------- | -------------- | -------- |
| localStroage     | 执行删除命令才 |          |
| sessionStorage   |                |          |

