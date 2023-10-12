# Commonlit2  　21th place solution🥈
[link](https://www.kaggle.com/competitions/commonlit-evaluate-student-summaries/overview)

## Task
3~12年生の学生が書いたサマリー（要約）の質を評価する。ソーステキストのアイディアや詳細をどの程度表現できているか、使用されている言語がどの程度明確で正確で流暢であるか評価するモデルを構築する。サマリーはcontentとwordingの2つの尺度によって評価される。

<br />

### 評価指標
MCRMSE

<br />

## 解法
![SUBIMAGE](png/subImage.png "SUBIMAGE")

<br />

### key points
- Grouped-LLRD (Layer Wise Learning Rate Decay)
- Freezing layers ([reference](https://www.kaggle.com/competitions/commonlit-evaluate-student-summaries/discussion/433754#2405543))

<br />
<br />

### models
| exp | input_text | model | pooling | freezing | maxlen |
---- | ---- | ---- | ---- | ---- | ----
055 | text+prompt_question+prompt_text | deberta-v3-large | cls | no | 1024
084 | text+prompt_question+prompt_text | deberta-v3-large | cls | 4 layer close | 1024
004 | prompt_title+sep+text_length+sep+prompt_question+sep+text | deberta-v3-base+lgbm | attention | no | 512


<br />
<br />

### Result
| exp | 39c16e | 3b9047 | ebad26 | 814d6b | cv | public | private
---- | ---- | ---- | ---- | ---- | ---- | ---- | ----
055 | 0.4768 | 0.5045 | 0.4461 | 0.5842 | 0.4948 | 0.466 | 0.471
084 | 0.4540 | 0.5154 | 0.4427 | 0.5830 | 0.4907 |  | 
004 | 0.4969 | 0.6589 | 0.4887 | 0.6354 | 0.5618 | 0.501 | 0.531
004+lgbm | 0.4730 | 0.5802 | 0.4592 | 0.5809 | 0.5197 | 0.449 | 0.481

<br />
<br />

## Final Submission
sub = (exp055*.4 + exp084*.6)*.7 + (exp004+lgbm)*.3

21 / 2106 位　🥈

CV : 0.4777

Public : 0.435

Private : 0.461

