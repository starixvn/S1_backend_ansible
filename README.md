#  BuildAgent aws cli install 安裝步驟

- `Step1`：透過 curl 把 aws cli zip 安裝包下載下來
```shell=
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

- `Step2` 執行解壓縮
```shell=
unzip awscliv2.zip
```

- `Step3` 安裝 aws cli
```shell=
sudo ./aws/install
```

- `Step4` 驗證安裝結果

```shell=
aws --version
```
> 如果沒有 Print aws version 可以登出再登入再次執行 `aws --version`


## 問題排除
- 如果沒有安裝過 curl 工具，可透過 <font color=red>`apt-get install curl`</font> 指令安裝
- 如果沒有安裝過 unzip 工具 ，可透過<font color=red>`apt-get install unzip`</font> 指令安裝
- [參考 aws 官方 aws cli install 教學](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)