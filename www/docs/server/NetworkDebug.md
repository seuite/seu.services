# 那些奇怪的bug和debug

- 故障：80端口无回应

  解决办法：

	    service firewalld stop

- nginx 403 forbidden

	关闭selinux即可

		setenforce 0


- 数据库和端口无反应
	检查设置和维护脚本名称是否命名正确:
		conf.yml config.yml config.toml

