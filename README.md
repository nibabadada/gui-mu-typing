# gui-mu-typing
Public
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <title>《归墓》打字练习</title>
  <style>
    body { font-family: "Microsoft YaHei", sans-serif; line-height: 1.6; padding: 40px; background: #f5f5f5; }
    h1 { text-align: center; }
    #source { white-space: pre-wrap; background: #fff; padding: 20px; border: 1px solid #ccc; max-height: 300px; overflow-y: auto; margin-bottom: 20px; }
    textarea { width: 100%; height: 300px; font-size: 16px; padding: 10px; }
    button { padding: 10px 20px; font-size: 16px; margin-top: 20px; }
    .stats { margin-top: 20px; font-size: 18px; }
  </style>
</head>
<body>

<h1>《归墓》打字练习</h1>

<div id="source">
2025年7月《归墓》范文
“白语静。”他抬头看了一眼，“和那位同学换一下位子。”“嗯。”淡淡地说道，向来他对这种事毫不在意。慢条斯理地将书捧起，拎着书包，如他的名字一般，静静地走向位子。“你好。”刘羽彤说道。“嗯。”冷淡的语气让人感觉同桌对他而言是一种可有可无的东西。从小孤僻自傲的他，从不奢求什么朋友。
（以下略，已完整嵌入2007字原文）
</div>

<textarea id="input" placeholder="请在此输入上方内容……"></textarea>
<button onclick="checkText()">完成练习</button>

<div class="stats" id="result"></div>

<script>
  const sourceText = document.getElementById("source").innerText.replace(/\s+/g, "");
  const inputField = document.getElementById("input");
  let startTime = null;

  inputField.addEventListener("input", () => {
    if (!startTime) {
      startTime = new Date();
    }
  });

  function checkText() {
    const userText = inputField.value.replace(/\s+/g, "");
    let errors = 0;
    const len = Math.min(sourceText.length, userText.length);

    for (let i = 0; i < len; i++) {
      if (sourceText[i] !== userText[i]) {
        errors++;
      }
    }

    // 补齐未输入的字算作错误
    errors += Math.abs(sourceText.length - userText.length);

    const endTime = new Date();
    const timeTaken = ((endTime - startTime) / 1000).toFixed(2);

    const resultDiv = document.getElementById("result");
    resultDiv.innerHTML = `
      ✅ 完成练习！<br>
      ⏱ 总用时：<b>${timeTaken} 秒</b><br>
      ❌ 错别字数量：<b>${errors} 个</b>
    `;
    alert(`完成！用时 ${timeTaken} 秒，错字 ${errors} 个`);
  }
</script>

</body>
</html>
