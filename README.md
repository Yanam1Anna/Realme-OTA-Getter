# 真我(Realme)系列手机 系统全量包 下载器 
![License](https://img.shields.io/github/license/R0rt1z2/realme-ota)
![GitHub Issues](https://img.shields.io/github/issues-raw/R0rt1z2/realme-ota?color=red)

---

## 配置要求
* Python 3.9 (或更高)。

---

## 安装
### Windows
* 需要管理员身份运行[Windows Terminal](https://github.com/microsoft/terminal) 或 [PowerShell](https://github.com/PowerShell/PowerShell)。

```powershell
Invoke-WebRequest https://raw.githubusercontent.com/R0rt1z2/realme-ota/master/Install.ps1 | Invoke-Expression
```

### Linux
```bash
sudo apt install python3-pip
pip3 install --upgrade git+https://github.com/R0rt1z2/realme-ota
```

---

## 使用方法
```bash
用法: realme-ota [-h] [-v {0,1,2,3,4,5} | -s] [-r {0,1,2,3}] [-g GUID] [-i IMEI [IMEI ...]] [-b] [-l LANGUAGE] [--old-method] [-d DUMP] [-o ONLY] product_model ota_version {1,2,3,4,5,6} [nv_identifier]

位置参数:
  product_model         产品型号 (ro.product.name)。
  ota_version           OTA 版本 (ro.build.version.ota)。
  {1,2,3,4,5,6}         RealmeUI 版本 (ro.build.version.realmeui)。
  nv_identifier         NV (运营商) 标识符 (ro.build.oplus_nv_id) (如果没有，请提供 0 或省略)。

选项:
  -h, --help            显示帮助信息并退出
  -v {0,1,2,3,4,5}, --verbosity {0,1,2,3,4,5}
                        设置日志级别。范围：0 (无日志) 到 5 (调试)。默认值：4 (信息)。
  -s, --silent          启用静默输出 (禁用日志记录)。-v0 的快捷方式。

请求选项:
  -r {0,1,2,3}, --region {0,1,2,3}
                        使用自定义区域进行请求 (全球 = 0, 中国 = 1, 印度 = 2, 欧洲 = 3)。
  -g GUID, --guid GUID  文件 /data/system/openid_config.xml 中的第三行 guid (仅在中国提取 'CBT' 时需要)。
  -i IMEI [IMEI ...], --imei IMEI [IMEI ...]
                        指定一个或两个 IMEI 进行请求。
  -b, --beta            尝试获取测试版本 (可能需要 IMEI)。
  -l LANGUAGE, --language LANGUAGE
                        指定响应的语言 (默认为 en-EN，中国为 zh-CN)。
  --old-method          使用旧方法进行请求 (仅适用于 rui_version >= 2)。

输出选项:
  -d DUMP, --dump DUMP  将请求响应保存到文件中。
  -o ONLY, --only ONLY  仅显示响应中的所需值。
```

---

## 使用示例
```python
realme-ota -r 1 RMX3300 RMX3300_11.F.00_0000_000000000000 5 10010111
```



| 代码                   | 含义                                                         |
| ---------------------- | ------------------------------------------------------------ |
| realme-ota             | 调用脚本                                                     |
| -r 1                   | 区域编号<br>国际版 = 0, 中国 = 1, 印度 = 2, 欧洲 = 3         |
| RMX3300                | 设备型号（在“关于本机”-“版本信息”中，“版本号”前面的字符串，不包含下划线及其后方内容） |
| RMX3300_11.            | 硬件版本号（格式：设备型号_数字）                            |
| F.00_0000_000000000000 | 字母表示版本类型，类型有以下几种：<br>A=出厂版本   C=跨代版本   F=末代版本<br>后方数字为ROM的版本号（后方数字全为0即为获取最新，其他请自行测试） |
| 5                      | realme ui的版本                                              |
| 10010111               | 区域的NV_ID（BIN），详情参与下方NV_ID表格，具体情况请自行测试 |

---

### NV_ID表:（引用源：[[Global/EU] Collection of firmware files](https://xdaforums.com/t/global-eu-collection-of-firmware-files.4478153/)）(所有机型通用)

|              国家/地区               |     区域缩写     | NV_ID (HEX) | NV_ID (BIN) | ROM 类型 | 注释  |
| :----------------------------------: | :--------------: | :---------: | :---------: | :------: | :---: |
|               中国台湾               |        TW        |     1A      |  00011010   |  export  |       |
|                 印度                 |        IN        |     1B      |  00011011   |  export  |       |
|              印度尼西亚              |        ID        |     33      |  00110011   |  export  |       |
|                俄罗斯                |        RU        |     37      |  00110111   |  export  |       |
|               马来西亚               |        MY        |     38      |  00111000   |  export  |       |
|                 泰国                 |        TH        |     39      |  00111001   |  export  |       |
|                菲律宾                |        PH        |     3E      |  00111110   |  export  |       |
|              沙特阿拉伯              |        SA        |     83      |  10000011   |  export  |       |
|               拉丁美洲               |      LATAM       |     9A      |  10011010   |  export  |       |
|                 巴西                 |        BR        |     9E      |  10011110   |  export  |       |
|              中东和非洲              |       MEA        |     A6      |  10100110   |  export  |       |
| 欧洲（欧盟，欧洲经济区，英国和瑞士） |       EUEX       |     44      |  01000100   |   GDPR   |       |
|                 英国                 |        GB        |     8A      |  10001010   |   GDPR   |   1   |
|                土耳其                |        TR        |     51      |  01010001   |   GDPR   |       |
|                 西欧                 | EU-NONEEA-Double |     8D      |  10001101   |   GDPR   |       |
|                 中国                 |      ALLNET      |     97      |  10010111   | domestic |       |

#### 注释:

1. 仅在版本 C.08 到 C.16 中（含）中找到；与 EUEX 相同，但有可能区分某些分区。

---

## 其他说明
* 如果您的请求返回`flow limit`或状态代码`500`，请尝试等待几分钟然后再次请求。
* 您可以使用`ALL_PROXY`环境变量通过代理发送请求（如果在您所在的国家/地区找不到更新，则很有用）。在 Windows 上，您可以运行`set ALL_PROXY=ADDRESS:PORT`，而在 Linux 和 MacOS 上，您可以执行`export ALL_PROXY=ADDRESS:PORT`。
* 自 Android 11 (Realme UI2) 以来，Realme 开始使用组件，这意味着您将无法获得完整的 OTA 链接。
* 该`--beta`选项可能无法正常工作，尚未经过全面测试！

## 协议
* 此工具根据 ` GPL-3.0 ` 通用公共许可证授权。 请参阅 ` LICENSE ` 了解更多信息。
