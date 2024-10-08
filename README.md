# 一个基于Cloudflare Workers运行的程序。用于安全地使用第三方的点阅转换服务。

本项目来自https://github.com/bulianglin/psub

原理是

节点信息先通过本程序将所有服务器地址和密码敏感信息替换为随机的值

再将处理后的节点信息交由第三方订阅转换服务做转换

拿到第三方转换后的节点信息，再统一恢复被替换的敏感信息

程序的运行需要在cloudflare配置以下信息

**环境变量**

在对应的workers项目中添加一个名为“BACKEND”的环境变量，此 环境变量用于配置第三方转换服的地址

**KV存储**（免费计划每天有1000次操作，理论上个人用户已经可以满足）

- 在KV中添加一个命名空间（名称可自定义），我这里假设是"**proxyConvert**"
  
![image](https://github.com/user-attachments/assets/13dc31aa-988e-4f3d-9879-5a288da98065)


- 在对应workers项目的【KV 命名空间绑定】中绑定刚才新建的KV命名空间（**proxyConvert**），注意绑定时的【变量名称】必须是"**SUB_BUCKET**"
  

	![image](https://github.com/user-attachments/assets/96c9fcbc-1f8e-4753-870e-3793dfc6c8bb)
