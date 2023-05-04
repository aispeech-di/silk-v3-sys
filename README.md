# Silk V3 decoder

## 介绍和说明

SILK是一种语音编码格式，由Skype公司研发，最后的版本发布时间为2012年。

**SILK** 原始代码已上传到 [Release](https://github.com/foyoux/pilk/releases/tag/v0.0.1) , 包含规范文档

### SILK编码格式和Tencent系语音的关系

1. 标准silk文件以`b'#!SILK_V3'` 开始，以`b'\xFF\xFF'` 结束，中间为语音数据。
2. 微信语音文件在标准SILK文件的开头插入了`b'\x02'`，去除了结尾的 `b'\xFF\xFF'`，中间不变。

**语音数据**

语音数据分为很多个独立  **frame** ，每个 **frame** 开头两字节存储剩余 **frame** 数据的大小，每个 **frame** 默认存储 **20ms** 的音频数据，

据此可通过程序计算出 **语音文件** 持续时间(duration) 的函数。

SILK格式规范，frame_ms 可分为20、40、60、80、100
