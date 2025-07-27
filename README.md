# THU-intern
该repo主要记录我在清华脑与智能实验室暑期实习的一些学习记录
大概包括EEGNET，模型的可解释性方法，EEGNET应用及相关可解释性分析等等\
**仅供学习参考，本人实力有限，不当之处尽可邮箱指正！**\
email：lzy123@bupt.edu.cn

## Depression Rest Classification
### data preprocessing
做一个四分类EEGNET，根据描述（数据来源于James F Cavanagh），使用所有患者的rest1静息态记录，去除544号受试者。四分类分别是MDD患者，DP（有抑郁情绪但是不是MDD也不是正常人的受试者），HC（健康对照组），past-MDD。\
MDD:11人，以SCID=1为标准\
DP：23人，以BDI分数>13为标准\
HC：75人\
past-MDD：12人以SCID=2为标准\
\
\
以507被试为例，先利用mne库读取文件放置raw中。可以通过打印raw.ch_names查看raw有哪些EEG channel。
<img width="300" height="500" alt="image" src="https://github.com/user-attachments/assets/873e8bed-dc8f-47eb-acc4-684a45d57239" />\
经过检验，所有被试的通道形式都为64EEG+2EOG（HEOG+VEOG，水平眼动和垂直眼动）
因为原EEG信号并未进行过滤波处理，所以此处我们浅显地采用一个带通滤波器,范围在（0.5~40Hz）\
\
\
可以通过json文件得知电网的工作频率是60Hz，<img width="200" height="25" alt="image" src="https://github.com/user-attachments/assets/999d1f09-ca96-4ddb-9150-08a8e3999983" />\
所以额外采用一次陷波滤波（notch-filter 60Hz）去除噪声\
接下来，我们需要找出“坏通道”（bad channels，简称‘bads’）。去除平线，极端噪声和剧烈漂移信号通道。可以利用mne.preprocessing的find_bad_channels_lof库直接进行操作。以标准差为检验标准，threshold=1.5，超过则认定为bads
