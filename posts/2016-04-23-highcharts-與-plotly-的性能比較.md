<!--
.. title: Highcharts 與 Plotly 的性能比較
.. slug: Highcharts 與 Plotly 的性能比較
.. date: 2016-04-23 10:37:26 UTC+08:00
.. tags: Highcharts, Plotly
.. category:
.. link:
.. description:
.. type: text
-->

Highcharts 與 Plotly 都是用來繪製網頁圖表的 JavaScript library 為了確認哪套比較適合在同一張圖表上繪製大量數組，我用 Plotly 與 Highcharts 繪製相同的大數組圖表，測試他們在顯示大量數組時的反應。

實驗發現(數組名稱較長情況下)

 - 在少量數組時，Highcharts 的游標移動效果較 Plotly 平順。
 - 隨著顯示數組的增加 Highcharts 順暢度開始遞減，而 Plotly 無明顯改變。
 - 當顯示所有數組時，Highcharts 幾乎動彈不得，Plotly 仍然可以正常操作。

額外發現

 - 數組名稱的長度對 Highcharts 有顯著影響，如減少數組名稱的長度，流暢度就會大幅提昇。
 - Plotly 無論名稱長短、數組多寡，都無太大差異。

結論

**如要繪製顯示大量數組的圖表，建議用 Plotly 較不會因數組名稱過長導致體驗變差。**

實驗 DEMO (30個數組、每組200個數值)

 - [Highcharts-大數組-長名稱](/2016-04-23-highcharts-與-plotly-的性能比較/highcharts_test_long.html)
 - [Highcharts-大數組-短名稱](/2016-04-23-highcharts-與-plotly-的性能比較/highcharts_test_short.html)
 - [Plotly-大數組-長名稱](/2016-04-23-highcharts-與-plotly-的性能比較/plotly_test_long.html)
 - [Plotly-大數組-短名稱](/2016-04-23-highcharts-與-plotly-的性能比較/plotly_test_short.html)

順便記錄用來產生測試數據的程式碼如下

```
import json, random
a1=[]
b1=[]

for x in range(30):
    labelsName='samplexxxxxxxxxxxxxx'+str(x)
    #labelsName='sample'+str(x)
    randint=[random.randint(1, 100) for _ in range(200)]
    #for plotly
    a={'type':'scatter','model':'lines','name':labelsName}
    a['y']=randint
    a1.append(a)

    #for highcharts
    b={}
    b['name']=labelsName
    #b['visible']= False
    b['data']=randint
    b1.append(b)

with open('plotly_test.json','w') as f:
    f.write(json.dumps(a1))

with open('highcharts_test.json','w') as f:
    f.write(json.dumps(b1))
```
