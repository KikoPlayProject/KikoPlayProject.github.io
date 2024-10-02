---
layout: post
title: "KikoPlay扩展App：AI字幕"
date:   2024-10-02 00:00:00
categories: extApp
---

AI字幕基于[whisper.cpp](https://github.com/ggerganov/whisper.cpp)，支持在本地直接为视频生成字幕，同时支持通过chatgpt对识别结果进行翻译。

下载地址：[百度云](https://pan.baidu.com/s/1gyT0FU9rioaa77znhAUx2w#list/path=%2FKikoPlay%2F%E6%89%A9%E5%B1%95App)

下载后解压放到`extension\app`目录下

## 使用方法
 
点击“打开文件”选择一个视频文件，或者直接选择KikoPlay正在播放的文件。如果只是想翻译字幕，也支持仅打开srt字幕文件：

![](/static/posts/24-10-02-1.jpg)

点击“识别字幕” 开始识别，如果提示“请在设置中指定whisper模型文件”，在设置页中先设置 whisper模型文件，默认携带了base版本模型（位于`model`目录）

![](/static/posts/24-10-02-2.jpg)

识别结束后可点击“翻译字幕”进行翻译（需要设置chatgpt api）：

![](/static/posts/24-10-02-3.jpg)

可直接双击识别结果进行修改。点击“保存字幕”可将结果保存为srt字幕文件，可保存原始/识别/双语结果：

![](/static/posts/24-10-02-4.jpg)

保存后可点击“载入KikoPlay”将字幕直接加载到KikoPlay正在播放的文件里。

## 设置

![](/static/posts/24-10-02-5.jpg)

 - 使用cuda加速whisper识别：如果系统安装了cuda，可勾选这个选项加速识别过程。（whisper.cpp加载相同的模型，cpu/gpu识别相同的文件可能有不同的结果）
 - whisper模型文件：默认打包了base版本的模型（位于`model`目录下），可以自行下载更大的模型（识别效果会更好）：[huggingface](https://huggingface.co/ggerganov/whisper.cpp/tree/main), [ggerganov](https://ggml.ggerganov.com/), [魔塔社区](https://www.modelscope.cn/models/cjc1887415157/whisper.cpp/files)
 - 视频语言识别：默认是"auto"，由whisper自动检测，如果检测不正确，可手动指定：(只输入:前面的部分)
   ```
    en: english,
    zh: chinese,
    de: german,
    es: spanish,
    ru: russian,
    ko: korean,
    fr: french,
    ja: japanese,
    pt: portuguese,
    tr: turkish,
    pl: polish,
    ca: catalan,
    nl: dutch,
    ar: arabic,
    sv: swedish,
    it: italian,
    id: indonesian,
    hi: hindi,
    fi: finnish,
    vi: vietnamese,
    he: hebrew,
    uk: ukrainian,
    el: greek,
    ms: malay,
    cs: czech,
    ro: romanian,
    da: danish,
    hu: hungarian,
    ta: tamil,
    no: norwegian,
    th: thai,
    ur: urdu,
    hr: croatian,
    bg: bulgarian,
    lt: lithuanian,
    la: latin,
    mi: maori,
    ml: malayalam,
    cy: welsh,
    sk: slovak,
    te: telugu,
    fa: persian,
    lv: latvian,
    bn: bengali,
    sr: serbian,
    az: azerbaijani,
    sl: slovenian,
    kn: kannada,
    et: estonian,
    mk: macedonian,
    br: breton,
    eu: basque,
    is: icelandic,
    hy: armenian,
    ne: nepali,
    mn: mongolian,
    bs: bosnian,
    kk: kazakh,
    sq: albanian,
    sw: swahili,
    gl: galician,
    mr: marathi,
    pa: punjabi,
    si: sinhala,
    km: khmer,
    sn: shona,
    yo: yoruba,
    so: somali,
    af: afrikaans,
    oc: occitan,
    ka: georgian,
    be: belarusian,
    tg: tajik,
    sd: sindhi,
    gu: gujarati,
    am: amharic,
    yi: yiddish,
    lo: lao,
    uz: uzbek,
    fo: faroese,
    ht: haitian creole,
    ps: pashto,
    tk: turkmen,
    nn: nynorsk,
    mt: maltese,
    sa: sanskrit,
    lb: luxembourgish,
    my: myanmar,
    bo: tibetan,
    tl: tagalog,
    mg: malagasy,
    as: assamese,
    tt: tatar,
    haw: hawaiian,
    ln: lingala,
    ha: hausa,
    ba: bashkir,
    jw: javanese,
    su: sundanese,
    yue: cantonese,
   ```
 - 启用VAD：支持基于[silero-vad](https://github.com/snakers4/silero-vad/tree/master)的vad检测，如果音频中包含较多空白影响whisper检测效果，可尝试开启。 

    开启后，在whisper识别前会执行vad检测，提取包含语音的片段合并后再由whisper识别，最终将识别结果映射会原始音频的位置。

    可调整 检测阈值、语音之间的最小空白、语音最少持续 三个选项来取得更好的检测效果。
 - ChatGPT API Key：可从[这里](https://github.com/chatanywhere/GPT_API_free)免费获取一个支持chatgpt 3.5的API Key，需要有github账户。
 - ChatGPT翻译Prompt：通过Prompt引导chatgpt进行翻译，可自行调整
 - ChatGPT每次请求翻译条数：条数越少请求次数越多，但条数多可能影响识别效果。
