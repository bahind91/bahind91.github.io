# bahind91.github.io

<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Genshin Impact Character Generator</title>
  <style>
    body {
      font-family: "Segoe UI", sans-serif;
      background: #1a1a1a;
      color: #f9f9f9;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }

    h1 {
      color: #ffd166;
    }

    #result {
      font-size: 1.8em;
      margin: 20px 0;
      color: #06d6a0;
    }

    button {
      background-color: #ef476f;
      color: white;
      border: none;
      padding: 12px 24px;
      font-size: 1em;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    button:hover {
      background-color: #d43d5c;
    }
  </style>
</head>
<body>
  <h1>🎲 Genshin Impact Character Generator</h1>
  <div id="result">Click the button to get a random character!</div>
  <button onclick="getRandomCharacter()">Get Character</button>

  <script>
    const genshinCharacters = [
      "Albedo", "Alhaitham", "Aloy", "Amber", "Arataki Itto", "Baizhu", "Barbara", "Beidou", "Bennett",
      "Candace", "Charlotte", "Chevreuse", "Chongyun", "Collei", "Cyno", "Dehya", "Diluc", "Diona", "Dori",
      "Eula", "Faruzan", "Fischl", "Freminet", "Furina", "Gaming", "Ganyu", "Gorou", "Hu Tao", "Jean",
      "Kaedehara Kazuha", "Kaeya", "Kamisato Ayaka", "Kamisato Ayato", "Kaveh", "Keqing", "Kirara", "Klee",
      "Kujou Sara", "Kuki Shinobu", "Layla", "Lisa", "Lynette", "Lyney", "Mika", "Mona", "Nahida", "Navia",
      "Neuvillette", "Nilou", "Ningguang", "Noelle", "Qiqi", "Raiden Shogun", "Razor", "Rosaria",
      "Sangonomiya Kokomi", "Sayu", "Shenhe", "Shikanoin Heizou", "Sucrose", "Tartaglia (Childe)", "Thoma",
      "Tighnari", "Traveler (Anemo)", "Traveler (Geo)", "Traveler (Electro)", "Traveler (Dendro)", "Venti",
      "Wanderer", "Wriothesley", "Xiangling", "Xianyun", "Xiao", "Xingqiu", "Xinyan", "Yae Miko", "Yanfei",
      "Yaoyao", "Yelan", "Yoimiya", "Yun Jin", "Zhongli", "Mualani", "Kinich", "Kachina", "Chasca", "Ororon",
      "Mavuika", "Citlali", "Lan Yan", "Varesa", "Iansan", "Escoffier", "Ifa", "Dahlia", "Akkefa"
    ];

    function getRandomCharacter() {
      const index = Math.floor(Math.random() * genshinCharacters.length);
      const name = genshinCharacters[index];
      document.getElementById("result").textContent = `✨ Your character is: ${name}`;
    }
  </script>
</body>
</html>
