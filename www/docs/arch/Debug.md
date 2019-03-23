## 如果git push提示没有远程仓库权限（public key)
检查当前用户
如果是非root账户，ssh-keygen生成的是当前账户的密钥
但是git push时由于要求sudo, 故使用的是root账户的密钥，因此生成密钥时应切换到root账户生成，即
```bash
$ sudo ssh-keygen
```