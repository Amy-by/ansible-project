
# **Ansible自动化配置管理系统**

## **项目简介**
本项目使用Vagrant和Ansible搭建一个多节点自动化管理环境，包含1个控制节点和2个被控节点（Web服务器和数据库服务器）。通过Ansible Playbook实现基础设施即代码（IaC），自动化完成软件安装、配置和服务部署，大幅提升运维效率。


## **技术栈**
- **虚拟化**：VirtualBox + Vagrant
- **自动化工具**：Ansible
- **操作系统**：Ubuntu 22.04 LTS
- **Web服务**：Nginx
- **数据库**：MariaDB (MySQL兼容)


## **项目结构**
```
ansible-project/
├── Vagrantfile               # 虚拟机配置文件
├── inventory/                # Ansible主机清单目录
│   └── hosts                 # 定义Web和DB节点
├── playbooks/                # Ansible Playbook目录
│   ├── web_setup.yml         # Web节点配置
│   ├── db_setup.yml          # DB节点配置
│   └── common_setup.yml      # 通用配置
└── .gitignore                # Git忽略文件
```


## **快速开始**

### **前置条件**
1. 安装 [VirtualBox](https://www.virtualbox.org/)
2. 安装 [Vagrant](https://www.vagrantup.com/)
3. 安装 [Git](https://git-scm.com/)


### **部署步骤**
1. **克隆仓库**
   ```bash
   git clone https://github.com/Amy-by/ansible-project.git
   cd ansible-project
   ```

2. **启动虚拟机**
   ```bash
   vagrant up
   ```

3. **登录控制节点**
   ```bash
   vagrant ssh ansible-control
   ```

4. **执行Ansible Playbooks**
   ```bash
   # 配置所有节点
   ansible-playbook -i ~/ansible/inventory/hosts ~/ansible/playbooks/common_setup.yml

   # 配置Web节点
   ansible-playbook -i ~/ansible/inventory/hosts ~/ansible/playbooks/web_setup.yml

   # 配置DB节点
   ansible-playbook -i ~/ansible/inventory/hosts ~/ansible/playbooks/db_setup.yml
   ```


## **验证部署**
1. **检查服务状态**
   ```bash
   # 检查Web节点Nginx状态
   ansible web -i ~/ansible/inventory/hosts -m service -a 'name=nginx state=started'

   # 检查DB节点MySQL状态
   ansible db -i ~/ansible/inventory/hosts -m service -a 'name=mariadb state=started'
   ```

2. **测试数据库连接**
   ```bash
   mysql -h <DB节点IP> -u test_user -p123456 -e 'SHOW DATABASES;'
   ```

3. **访问Web服务**
   在浏览器中打开：`http://<Web节点IP>`
   你应该看到"Web节点 - 1"的页面，中文显示正常。


## **项目特点**
1. **免密SSH认证**：通过SSH密钥自动配置控制节点与被控节点的信任关系
2. **模块化设计**：Playbook按功能拆分，便于维护和扩展
3. **中文支持**：Nginx配置中添加UTF-8编码支持，确保中文正常显示
4. **远程访问**：数据库配置允许远程连接，便于开发和管理
5. **环境变量**：统一配置环境变量，方便应用部署


## **常见问题**
1. **网络连接问题**
   - 确保Vagrantfile中的`bridge`参数与你的物理网卡名称一致
   - 检查虚拟机是否获取到正确的IP地址

2. **Ansible执行失败**
   - 确认控制节点与被控节点之间的SSH连接正常
   - 检查inventory/hosts文件中的IP地址是否正确

3. **数据库连接失败**
   - 确保DB节点的MariaDB服务已启动
   - 检查防火墙设置，确保3306端口开放


## **贡献指南**
1. Fork本仓库
2. 创建你的特性分支 (`git checkout -b feature/new-feature`)
3. 提交你的更改 (`git commit -am 'Add some feature'`)
4. 将分支推送到远程仓库 (`git push origin feature/new-feature`)
5. 创建Pull Request


