# hfyzdns.cn 全量备份

合肥一中电脑社网站全量备份（加密分卷）。

## 内容
- `part_aa` ~ `part_ak`：加密备份分卷（openssl aes-256-cbc，密码见 backup.sh / 运维手册）
- `SHA256SUMS`：分卷校验和

## 还原
1. `cat part_* > full-backup.tar.gz.aes`
2. `sha256sum -c SHA256SUMS`
3. 解密：`openssl enc -d -aes-256-cbc -salt -pbkdf2 -pass pass:<密码> -in full-backup.tar.gz.aes | tar xz`

备份范围：网站业务数据 + nginx 配置 + crontab + OpenClaw workspace/配置/状态 + AI 代码（排除 node_modules/models/缓存）。
