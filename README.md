
# Ansible EDA Demo - 唐詩300首小品

# 環境準備
  Ansible AAP Controller
  Ansible EDA Controller

# 使用方法
1. 建立 AAP User Token

2. 建立 Job Template 並且新增下列參數

```
keyword: "{{ ansible_eda.event.payload.keyword }}"
jsondata: "{{ lookup('file', '300-zh_tw.json') | from_json }}"

```

3. EDA 建立 Creditial (步驟1 的 AAP User Token)

4. EDA 建立 Project

5. EDA 建立 Rulebook Activations

6. 使用下列指令傳送要查詢唐詩300首內容中的關鍵字

```
curl -X POST -H "Content-Type: application/json" -d '{"keyword": "黃河"}' < EDA_IP_ADDRESS >:5050
```

7. 確認 EDA Rulebook Activations history 訊息

```
2024-07-10 09:43:15,805 - ansible_rulebook.rule_set_runner - INFO - Waiting for events, ruleset: Example
2024-07-10 09:43:15,889 - ansible_rulebook.websocket - INFO - feedback websocket connected
2024-07-10 09:43:55,255 - aiohttp.access - INFO - 10.0.2.100 [10/Jul/2024:09:43:55 +0000] "POST / HTTP/1.1" 200 150 "-" "curl/7.61.1"
2024-07-10 09:43:55,336 - ansible_rulebook.action.run_job_template - INFO - running job template: zen-300, organization: EDA展示區
2024-07-10 09:44:07,064 - ansible_rulebook.action.run_job_template - INFO - job results url: https://tower.experteam.com.tw/#/jobs/2805/details
``` 

8. Ansible AAP 執行 JOB 結果

```
PLAY [Tang Poems Search] *******************************************************
TASK [Gathering Facts] *********************************************************
ok: [localhost]
TASK [Print Solgon] ************************************************************
ok: [localhost] => {
    "msg": "熟讀唐詩三百首，不會作詩也能吟。"
}
TASK [Display inputs] **********************************************************
ok: [localhost] => {
    "msg": "搜尋的關鍵字詞: 黃河"
}
TASK [Print Search Result] *****************************************************
ok: [localhost] => {
    "msg": [
        {
            "author": "李白",
            "contents": "金樽清酒鬥十千，玉盤珍羞值萬錢。\n停杯投箸不能食，拔劍四顧心茫然。\n欲渡黃河冰塞川，將登太行雪滿山。\n閒來垂釣碧溪上，忽復乘舟夢日邊。\n行路難，行路難！多歧路，今安在？\n長風破浪會有時，直掛雲帆濟滄海。",
            "id": 82,
            "title": "行路難三首之一",
            "type": "七言樂府"
        },
        {
            "author": "李白",
            "contents": "君不見，黃河之水天上來，奔流到海不復回。\n君不見，高堂明鏡悲白髮，朝如青絲暮成雪。\n人生得意須盡歡，莫使金樽空對月！\n天生我材必有用，千金散盡還復來。\n烹羊宰牛且為樂，會須一飲三百杯！\n岑夫子，丹丘生，將進酒，君莫停！\n與君歌一曲，請君為我側耳聽！\n鐘鼓饌玉不足貴，但願長醉不願醒！\n古來聖賢皆寂寞，惟有飲者留其名！\n陳王昔時宴平樂，鬥酒十千恣歡謔。\n主人何為言少錢？徑須沽取對君酌。\n五花馬，千金裘，呼兒將出換美酒，與爾同消萬古愁！",
            "id": 85,
            "title": "將進酒",
            "type": "七言樂府"
        },
        {
            "author": "王之渙",
            "contents": "白日依山盡，黃河入海流。\n欲窮千里目，更上一層樓。",
            "id…
PLAY RECAP *********************************************************************
localhost                  : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 

``` 


