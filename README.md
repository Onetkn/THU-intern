# THU-intern
该repo主要记录我在清华暑期实习的一些学习记录
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
