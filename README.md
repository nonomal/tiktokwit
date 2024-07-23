# Tiktokwit: 使用LLM Agent的反思原理实现自动视频翻译

<p align="center">
  <a href="./README_EN.md">English</a> |
  <a href="./README.md">简体中文</a> |
</p>

## 项目介绍
- 本项目利用LLM Agent的反思机制，通过校验翻译结果控制翻译的时长，实现音视频的自动同步和高质量翻译。
- 经过实测，项目目前能够实现中文到英文、法文、葡萄牙文、西班牙文、德文、俄语的自动翻译，以及英文到法文、葡萄牙文、西班牙文、德文、俄语的自动翻译，其他语言暂未测试。

## 与同类项目的异同
- 现在同类项目多数自动翻译项目通过拉长或缩短音视频来实现同步，这会导致音频时快时慢。
- 本项目通过LLM Agent的反思机制，校验翻译结果并控制每段字幕的翻译时长，实现翻译后音频和视频的同步，保证翻译后的音频文件和视频文件的时长误差不超过300ms。


### 项目步骤说明
1. **视频转音频**
   - 将视频文件转换为MP3格式的音频文件。
   - 上传生成的音频文件并获取其URL。
   - 记录生成的MP3文件路径和URL。

2. **提取音频中的背景音**
   - 从转换后的音频文件中提取背景音，生成一个新的MP3文件。
   - 记录生成的背景音MP3文件路径。

3. **音频转字幕文件**
   - 将音频文件转换为中文字幕文件。
   - 检测字幕文件的语言，如果与目标语言相同，则抛出异常。
   - 检查字幕文件是否为空，为空则返回失败。
   - 插入空白字幕，如有需要。

4. **翻译字幕文件**
   - 将中文字幕文件翻译为目标语言的字幕文件。
   - 调整字幕文件中的空白字符行。
   - 检查中英文字幕段落数目是否一致，不一致则重试3次。

5. **生成目标语言的音频文件**
   - 将目标语言的字幕文件转换为音频文件。

6. **校验字幕文件**
   - 合并中英文字幕文件信息为CSV文件。
   - 根据CSV文件验证目标语言的音频文件。
   - 合并校验后的音频文件。

7. **合并语音和视频**
   - 将目标语言的音频文件与背景音视频文件合并，生成最终的视频文件。

8. **生成最终的字幕文件**
   - 根据CSV文件生成目标语言的字幕文件。

9. **烧录字幕和视频**
   - 将目标语言的字幕和视频烧录在一起，生成带时间戳的最终文件。

## 该项目已经提供核心代码
- 该项目的saas版本已经上线，https://mp4.tiktokwit.com/ 欢迎大家试用。
- 现在版本是较为完善的版本，是 alex.cai 和 WTWT.He 过去几个月在努力的结果，另外还有合作者（xianyu）帮助构建商业化版本的前端界面。
- 感谢大家对本项目的支持，希望更多人能够参与进来。

## 入门
### 1.安装依赖
暂时只支持在windows上运行，Mac和Linux需要自行解决FFmpeg的安装问题。
FFmpeg的Windows请参考网上的安装步骤

```sh
pip install -r requirements.txt
```

### 2.SysConfig文件中配置参数
包括火山引擎的各类API的参数 和OpenAI的API参数

### 3.运行Run.py
```sh
python Run.py
```

## 许可证

本仓库遵循 [Tiktokwit Open Source License](https://github.com/caixikai/tiktokwit/blob/main/LICENSE) 开源协议。

- 允许作为后台服务直接商用，但不允许提供 SaaS 服务。
- 未经商业授权，任何形式的商用服务均需保留相关版权信息。

完整请查看 [Tiktokwit Open Source License](https://github.com/caixikai/tiktokwit/blob/main/LICENSE)

联系方式：caixikai01@gmail.com


## 扩展的想法
以下是我们还没有时间去尝试但希望开源社区能够尝试的想法：

1. 尝试其他 LLM。我们主要使用 gpt-4-o 对此进行了原型设计。我们希望其他人可以尝试其他LLM,看看它们的翻译效果如何，我已经尝试过GPT-3.5和其他一些LLM，提示词可能需要做进一步的调整。
2. 大家可以尝试参考吴恩达老师的translation-agent对本项目代码做进一步的修改。
3. 对于亚洲语系，openai输出日文和韩文语音文件测试效果不理想。

# 社区交流群
<img src="https://github.com/caixikai/tiktokwit/blob/main/weixin.jpg?raw=true" alt="微信群二维码" width="500">

# 视频演示
所有demo视频都在tiktokwit/demomp4/这个目录下面

