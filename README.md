# bahind91.github.io


<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Random Name Generator</title>
  <style>
    body { font-family: sans-serif; padding: 2rem; background: #f0f0f0; text-align:center; }
    select, button { font-size: 1rem; padding: 0.5rem; margin: 1rem 0; }
    #result { font-size: 1.5rem; margin-top: 1rem; color: #333; }
    h1 { color: #222; }
  </style>
</head>
<body>
  <h1>Random Name Generator</h1>

  <button onclick="generateName()">Generate Character + Breed</button>
  <div id="result"></div>

  <script>
    // Genshin characters with associated model sizes (example data)
    // You need to fill in the correct sizes for all characters
    const genshinCharacters = [
      { name: "Albedo", model: "Medium Male" },
      { name: "Alhaitham", model: "Medium Male" },
      { name: "Aloy", model: "Medium Female" },
      { name: "Amber", model: "Medium Female" },
      { name: "Arlecchino", model: "Tall Female" },
      { name: "Ayaka", model: "Medium Female" },
      { name: "Ayato", model: "Medium Male" },
      { name: "Baizhu", model: "Medium Male" },
      { name: "Barbara", model: "Short Female" },
      { name: "Beidou", model: "Tall Female" },
      { name: "Bennett", model: "Medium Male" },
      { name: "Candace", model: "Tall Female" },
      { name: "Charlotte", model: "Medium Female" },
      { name: "Chasca", model: "Medium Female" },
      { name: "Chevreuse", model: "Tall Female" },
      { name: "Chiori", model: "Medium Female" },
      { name: "Chongyun", model: "Medium Male" },
      { name: "Citlali", model: "Medium Female" },
      { name: "Clorinde", model: "Tall Female" },
      { name: "Collei", model: "Short Female" },
      { name: "Cyno", model: "Medium Male" },
      { name: "Dehya", model: "Tall Female" },
      { name: "Diluc", model: "Tall Male" },
      { name: "Diona", model: "Short Female" },
      { name: "Dori", model: "Short Female" },
      { name: "Emilie", model: "Medium Female" },
      { name: "Escoffier", model: "Medium Male" },
      { name: "Eula", model: "Tall Female" },
      { name: "Faruzan", model: "Medium Female" },
      { name: "Fischl", model: "Medium Female" },
      { name: "Freminet", model: "Medium Male" },
      { name: "Furina", model: "Medium Female" },
      { name: "Gaming", model: "Medium Male" },
      { name: "Ganyu", model: "Medium Female" },
      { name: "Gorou", model: "Medium Male" },
      { name: "Heizou", model: "Medium Male" },
      { name: "Hu Tao", model: "Medium Female" },
      { name: "Iansan", model: "Medium Female" },
      { name: "Ifa", model: "Medium Female" },
      { name: "Itto", model: "Tall Male" },
      { name: "Jean", model: "Tall Female" },
      { name: "Kachina", model: "Medium Female" },
      { name: "Kaeya", model: "Tall Male" },
      { name: "Kaveh", model: "Medium Male" },
      { name: "Kazuha", model: "Medium Male" },
      { name: "Keqing", model: "Medium Female" },
      { name: "Kinich", model: "Medium Male" },
      { name: "Kirara", model: "Short Female" },
      { name: "Klee", model: "Short Female" },
      { name: "Kokomi", model: "Medium Female" },
      { name: "Lan Yan", model: "Medium Female" },
      { name: "Layla", model: "Medium Female" },
      { name: "Lisa", model: "Medium Female" },
      { name: "Lynette", model: "Medium Female" },
      { name: "Lyney", model: "Medium Male" },
      { name: "Mavuika", model: "Medium Female" },
      { name: "Mika", model: "Short Female" },
      { name: "Mizuki", model: "Short Female" },
      { name: "Mona", model: "Medium Female" },
      { name: "Mualani", model: "Medium Female" },
      { name: "Nahida", model: "Short Female" },
      { name: "Navia", model: "Medium Female" },
      { name: "Neuvillette", model: "Medium Male" },
      { name: "Nilou", model: "Medium Female" },
      { name: "Ningguang", model: "Medium Female" },
      { name: "Noelle", model: "Tall Female" },
      { name: "Ororon", model: "Medium Male" },
      { name: "Qiqi", model: "Short Female" },
      { name: "Raiden", model: "Tall Female" },
      { name: "Razor", model: "Tall Male" },
      { name: "Rosaria", model: "Tall Female" },
      { name: "Sara", model: "Medium Female" },
      { name: "Sayu", model: "Short Female" },
      { name: "Sethos", model: "Medium Male" },
      { name: "Shenhe", model: "Tall Female" },
      { name: "Shinobu", model: "Short Female" },
      { name: "Sigewinne", model: "Medium Female" },
      { name: "Sucrose", model: "Short Female" },
      { name: "Tartaglia", model: "Medium Male" },
      { name: "Thoma", model: "Medium Male" },
      { name: "Tighnari", model: "Medium Male" },
      { name: "Traveler (Anemo)", model: "Medium Male" },
      { name: "Traveler (Dendro)", model: "Medium Male" },
      { name: "Traveler (Electro)", model: "Medium Male" },
      { name: "Traveler (Geo)", model: "Medium Male" },
      { name: "Traveler (Hydro)", model: "Medium Male" },
      { name: "Traveler (Pyro)", model: "Medium Male" },
      { name: "Varesa", model: "Medium Female" },
      { name: "Venti", model: "Medium Male" },
      { name: "Wanderer", model: "Medium Male" },
      { name: "Wriothesley", model: "Tall Male" },
      { name: "Xiangling", model: "Medium Female" },
      { name: "Xianyun", model: "Medium Female" },
      { name: "Xiao", model: "Medium Male" },
      { name: "Xilonen", model: "Medium Female" },
      { name: "Xingqiu", model: "Medium Male" },
      { name: "Xinyan", model: "Medium Female" },
      { name: "Yae Miko", model: "Medium Female" },
      { name: "Yanfei", model: "Medium Female" },
      { name: "Yaoyao", model: "Short Female" },
      { name: "Yelan", model: "Medium Female" },
      { name: "Yoimiya", model: "Medium Female" },
      { name: "Yun Jin", model: "Medium Female" },
      { name: "Zhongli", model: "Tall Male" }
    ];

    const horseBreeds = [
      "Abaga", "Abyssinian", "Adaev", "Aegidienberger", "Akhal-Teke",
      "Albanian", "Altai", "Alter Real", "American Bashkir Curly", "American Belgian Draft",
      "American Cream Draft", "American Indian Horse", "American Paint Horse", "American Quarter Horse",
      "American Saddlebred", "American Warmblood", "Andalusian", "Andravida", "Anglo-Arabian",
      "Anglo-Kabarda", "Appaloosa", "Arabian", "Ardennais", "Arenberg-Nordkirchen", "Asturcón",
      "Australian Draught", "Australian Stock Horse", "Austrian Warmblood", "Auvergne", "Auxois",
      "Axios", "Azerbaijan", "Azteca", "Baise horse", "Bale",
      "Balikun horse", "Baluchi horse", "Banker horse",
      "Barb horse", "Bardigiano", "Bashkir horse", "Basque Mountain Horse", "Bavarian Warmblood",
      "Belgian Draught", "Belgian Sport Horse", "Belgian Trotter",
      "Belgian Warmblood", "Bhutia Horse", "Black Forest Horse", "Blazer horse", "Boerperd", "Borana", "Bosnian Mountain Horse",
      "Boulonnais horse", "Brandenburger", "Brazilian Sport Horse", "Breton horse",
      "British Warmblood", "Brumby", "Budyonny horse", "Burguete horse", "Burmese Horse",
      "Byelorussian Harness Horse", "Calabrese horse", "Camargue horse", "Camarillo White Horse", "Campeiro",
      "Campolina", "Canadian horse", "Canadian Pacer", "Carolina Marsh Tacky", "Carthusian Spanish horse",
      "Caspian horse", "Castillonnais", "Catria horse", "Cavallo Romano della Maremma Laziale",
      "Cerbat Mustang", "Chaidamu horse", "Chakouyi", "Chernomor horse",
      "Chilean horse", "Chinese Mongolian horse", "Choctaw horse", "Cleveland Bay", "Clydesdale horse",
      "Colorado Ranger", "Coldblood trotter", "Comtois horse", "Corsican horse", "Costa Rican Saddle Horse",
      "Criollo horse", "Croatian Coldblood", "Cuban Criollo", "Cumberland Island horse",
      "Czech Warmblood", "Danube Delta horse", "Datong horse", "Dølehest", "Dutch Harness Horse", "Dutch Draft",
      "Dutch Warmblood", "East Bulgarian", "Estonian Draft", "Estonian Native",
      "Ethiopian horses", "Falabella", "Finnhorse", "Flemish Horse", "Fleuve", "Fjord horse", "Florida Cracker Horse", "Foutanké",
      "Frederiksborger", "Freiberger", "French Trotter", "Friesian", "Furioso-North Star", "Galiceno",
      "Gelderland horse", "Giara Horse", "Gidran", "Groningen Horse", "Hackney horse", "Haflinger", "Hanoverian horse",
      "Heck horse", "Heihe horse", "Henson horse", "Hequ horse", "Hirzai", "Hispano-Bretón", "Hispano-Árabe",
      "Holsteiner", "Horro", "Hungarian Warmblood", "Icelandic horse", "Indian Country-bred", "Iomud", "Irish Draught",
      "Irish Sport Horse", "Italian Heavy Draft", "Italian Trotter", "Jaca Navarra", "Jeju horse", "Jutland horse",
      "Kabarda horse", "Kafa", "Kaimanawa horses", "Kalmyk horse", "Karabair",
      "Karabakh horse", "Karachai horse", "Kathiawari horse",
      "Kazakh Horse", "Kentucky Mountain Saddle Horse", "Kiger Mustang", "Kinsky horse", "Konik", "Kyrgyz Horse",
      "Kisber Felver", "Kiso Horse", "Kladruber", "Knabstrupper", "Kundudo horse", "Kurdish horse", "Kustanair",
      "Latvian horse", "Lipizzan", "Lithuanian Heavy Draught", "Ljutomer Trotter", "Lokai", "Losino horse",
      "Lusitano", "Luxembourg Warmblood", "M'Bayar", "M'Par", "Malopolski",
      "Mallorquín", "Mangalarga", "Mangalarga Marchador", "Marismeño", "Marwari horse", "Messara horse",
      "Missouri Fox Trotter", "Misaki horse", "Mokara pony", "Mongolian horse", "Morab",
      "Morocco horse", "Mustang", "New Forest pony", "Nonius", "Noriker",
      "Norwegian Fjord horse", "North Swedish horse", "Nova Scotia Duck Tolling Retriever horse",
      "Oldenburg horse", "Orlov trotter", "Ossetian horse", "Ostfriesen and Alt-Oldenburger",
      "Paso Fino", "Paso Peruano", "Percheron", "Peruvian Paso", "Persian horse",
      "Pindos horse", "Pinsk horse", "Posavac horse", "Pottok", "Przewalski's horse", "Pura Raza Española",
      "Pyrenean Horse", "Quarter horse", "Raidi horse", "Red Hare",
      "Rhenish German Coldblood", "Rocky Mountain horse", "Romanian Sport Horse",
      "Russian Don", "Russian Heavy Draft", "Russian Trotter", "Russian Riding Horse",
      "Sable Island horse", "Sakhalin horse", "Sangamneri", "Sardinian Anglo-Arab", "Selle Français",
      "Senner horse", "Shetland pony", "Siberian horse", "Silesian horse", "Sorraia horse",
      "South German Coldblood", "Spanish Mustang", "Standardbred", "Suffolk Punch",
      "Svalbard pony", "Swedish Ardennes horse", "Swedish Warmblood", "Swiss Warmblood",
      "Tennessee Walking Horse", "Theresian horse", "Thoroughbred",
      "Timber horse", "Tinker horse", "Tobiano horse", "Tornjak horse", "Tori horse",
      "Trakehner", "Trotter", "Tyrolean Haflinger", "Ukrainian Saddle horse", "Uruguayan Criollo",
      "Vanner horse", "Värmland horse", "Virginia Highlander", "Waler horse", "Westphalian horse",
      "Western Riding horse", "Württemberger horse", "Yakutian horse", "Yili horse", "Zaniskari horse"
    ];

    const ponyBreeds = [
      "Australian Pony", "British Riding Pony", "Chincoteague Pony", "Connemara Pony",
      "Dartmoor Pony", "Exmoor Pony", "Falabella", "Fell Pony",
      "Haflinger", "Highland Pony", "Hokkaido Pony", "Icelandic Pony",
      "Kerry Bog Pony", "Kiso Pony", "New Forest Pony", "Norfolk Pony",
      "Pony of the Americas", "Shetland Pony", "Sokoke Pony", "Welsh Pony"
    ];

    function generateName() {
      // Pick a random Genshin character
      const charIndex = Math.floor(Math.random() * genshinCharacters.length);
      const character = genshinCharacters[charIndex];
      const model = character.model;

      let breed = "";

      if (model.includes("Tall")) {
        // Tall: only horse breeds
        breed = horseBreeds[Math.floor(Math.random() * horseBreeds.length)];
      } else if (model.includes("Short")) {
        // Short: only pony breeds
        breed = ponyBreeds[Math.floor(Math.random() * ponyBreeds.length)];
      } else {
        // Medium: either horse or pony
        const allBreeds = horseBreeds.concat(ponyBreeds);
        breed = allBreeds[Math.floor(Math.random() * allBreeds.length)];
      }

      // Show both character and breed
      const resultDiv = document.getElementById("result");
      resultDiv.innerHTML = `
        <p><strong>Character:</strong> ${character.name} </p>
        <p><strong>Breed:</strong> ${breed}</p>
      `;
    }
  </script>
</body>
</html>

