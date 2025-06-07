# bahind91.github.io

<!DOCTYPE html>
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
  <label for="category">Choose a category:</label>
  <br />
  <select id="category">
    <option value="genshin">Genshin Impact Character</option>
    <option value="horse">Horse Breed</option>
    <option value="pony">Pony Breed</option>
  </select>
  <br />
  <button onclick="generateName()">Generate Name</button>
  <div id="result"></div>

  <script>
    const genshinCharacters = [
      "Albedo", "Alhaitham", "Aloy", "Amber", "Arataki Itto", "Arlecchino", "Ayaka", "Ayato",
      "Baizhu", "Barbara", "Beidou", "Bennett",
      "Candace", "Charlotte", "Chasca", "Chevreuse", "Chiori", "Chongyun", "Citlali", "Clorinde", "Collei",
      "Dehya", "Diluc", "Diona", "Dori",
      "Eula", "Emilie", "Escoffier",
      "Faruzan", "Fischl", "Freminet", "Furina",
      "Gaming", "Ganyu", "Gorou",
      "Heizou", "Hu Tao",
      "Ifa", "Iansan",
      "Jean",
      "Kaedehara Kazuha", "Kaeya", "Kamisato Ayaka", "Kamisato Ayato", "Kaveh", "Keqing", "Kirara", "Klee", "Kujou Sara", "Kuki Shinobu",
      "Layla", "Lisa", "Lynette", "Lyney",
      "Mika", "Mona",
      "Navia", "Neuvillette", "Nilou", "Ningguang", "Noelle",
      "Qiqi",
      "Raiden Shogun", "Razor", "Rosaria",
      "Sangonomiya Kokomi", "Sayu", "Shenhe", "Shikanoin Heizou", "Shinobu", "Sucrose",
      "Tartaglia (Childe)", "Thoma", "Tighnari", "Traveler",
      "Venti",
      "Wanderer", "Wriothesley",
      "Xiangling", "Xianyun", "Xiao", "Xingqiu", "Xinyan",
      "Yae Miko", "Yanfei", "Yaoyao", "Yelan", "Yoimiya", "Yun Jin",
      "Zhongli"
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
      const category = document.getElementById("category").value;
      let list;
      if (category === "genshin") {
        list = genshinCharacters;
      } else if (category === "horse") {
        list = horseBreeds;
      } else if (category === "pony") {
        list = ponyBreeds;
      }
      const randomIndex = Math.floor(Math.random() * list.length);
      const randomName = list[randomIndex];
      document.getElementById("result").textContent = randomName;
    }
  </script>
</body>
</html>
