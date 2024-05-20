<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Poem Visualizer</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: "Yu Gothic", sans-serif;
      font-weight: 250;
    }
  </style>
</head>
<body>
  <script>
    let nouns = [
      ["両目", "悲惨さ", "目的", "粘土", "国"],
      ["光", "影", "輝き", "明かり", "嘘"],
      ["画像", "代入可能性", "二人がけの机", "二人", "二人は"],
      ["ベッド", "サルベージ", "ソファ", "キメラ", "フェルト"],
      ["解除", "男", "断片", "ブリーチ", "リリース", "沈黙", "無音", "無声"],
      ["触覚", "スクリーン", "ビラ"],
      ["政治活動", "集会","ポーザー", "トイ", "原寸大"],
      ["手", "腕", "肩", "胸", "背中", "うで"],
      ["喉", "舌", "口", "顎", "歯"],
      ["可動性", "動かせる範囲", "身体", "振動", "動かせなさ"]
    ];

    let poem = [
      { fixedText: "遠くに見える", x: 65, nounIndex: 0 },
      { fixedText: "であったり", x: 200, nounIndex: 1 },
      { fixedText: "を集め終えた", x: 350, nounIndex: 2 },
      { fixedText: "は可視的になりすぎている", x: 480, nounIndex: 3 },
      { fixedText: "目の前にある草でさえも", x: 50, nounIndex: 4 },
      { fixedText: "のせいで感じられない", x: 200, nounIndex: 5 },
      { fixedText: "匿名な", x: 350, nounIndex: 6 },
      { fixedText: "を叩きつける", x: 500, nounIndex: 7 },
      { fixedText: "選択された", x: 32, nounIndex: 8 },
      { fixedText: "・", x: 200, nounIndex: 9 },
      { fixedText: "座りすぎだった", x: 350, nounIndex: 0 },
      { fixedText: "は許されていく", x: 500, nounIndex: 1 },
      { fixedText: "指先に", x: 53, nounIndex: 2 },
      { fixedText: "を押し当てた", x: 200, nounIndex: 7 },
      { fixedText: "動かせる範囲になる", x: 430, nounIndex: 4 }
    ];

    let cursorX, cursorY;

    function setup() {
      createCanvas(800, 800);
      textAlign(LEFT, CENTER);
      textSize(50);
      textStyle(NORMAL);
      frameRate(20);
    }

    function draw() {
      background(255);

      // マウスカーソルの位置を取得
      cursorX = mouseX;
      cursorY = mouseY;

      for (let i = 0; i < poem.length; i++) {
        let line = poem[i];
        text(line.fixedText, line.x, 50 + i * 40);
        let replacedText = replaceNoun(line.nounIndex);
        let x = line.x + textWidth(line.fixedText);
        let y = 50 + i * 40;
        let size = random(3, 22);
        textSize(size);

        // マウスカーソルに向かってテキストを引っ張る
        let angle = atan2(cursorY - y, cursorX - x);
        let newX = x + cos(angle) * 90;
        let newY = y + sin(angle) * 90;

        text(replacedText, newX, newY);
      }
    }

    function replaceNoun(nounIndex) {
      let randomNoun = random(nouns[nounIndex]);
      return randomNoun;
    }
  </script>
</body>
</html>
