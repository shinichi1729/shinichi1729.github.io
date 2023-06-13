---
layout: page
title: TOEIC L&Rテスト でるかも1000問
permalink: /myderusen
---

- 経緯など
    - 経緯
        - 大学院の講義課題のため作りました。←「NLPの技術を用いて何か作り発表」
        - テーマ選びについて..ネット上にPart5形式の問題がほとんどなかったから。
        - [TOEIC Part5の某参考書](https://www.amazon.co.jp/TOEIC-L-R%E3%83%86%E3%82%B9%E3%83%88-%E6%96%87%E6%B3%95%E5%95%8F%E9%A1%8C-%E3%81%A7%E3%82%8B1000%E5%95%8F/dp/4866390832)っぽい見た目をしていますが違います。

    - 使った技術
        - データは数個のゴールドデータを元にGPT3.5-turboを使用し生成しました。
        - 上記の処理はPythonで書き上げて、UI部分はJavasciptを使いました。
        
    - 改善すること (時間があれば)
        - 1000個と言ったが1000個作っていない
        - 文章の尤もらしさを定量的に判断して答えが一意的な問題のみ抽出。(perplexity?)


### 注意点

*問題文と選択肢は数個を除いて、GPT3.5に自動生成させています。<br>
(真偽について怪しい部分があると思います)

*生成方法などはGithubに今後載せます

<br>

---

<br>

<link rel="stylesheet" href="./toeic/toeic.css">

<script src="./toeic/toeic.js">
</script>
<audio id="correct-answer">
    <source src="./toeic/audio/correct.mp3" type="audio/mp3">
</audio>
<audio id="wrong-answer">
    <source src="./toeic/audio/wrong.mp3" type="audio/mp3">
</audio>
<script type="text/javascript">
    let problem_number;
    for (var i = 0; i < problems.length; i++) {
        if (i + 111 < problems.length){
            problem_number = i+1;
        }else{
            problem_number = 1000 - (problems.length - i - 1);
        }
        document.write("<div class='question-container'>");
        document.write ("<p> Q",problem_number, "." ,problems[i], "<p>");
        document.write("<ul>")
        const correct_answer = answers[i];
        let thisiscorrect, button_id;
        for (var k = 0; k < choices[i].length; k++){
            button_id = ('000' + (i+1)).slice(-4) + '-' + k;
            thisiscorrect = (choices[i][k] === correct_answer);
            document.write(`<button id=${button_id} class='button-002' onclick='onclickevent(this, ${thisiscorrect}, ${i+1})'> ${idx2alp[k]} ${choices[i][k]} </button>`);
        }
        document.write("</ul>")
        document.write("</div>");
    }

</script>
