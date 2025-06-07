# bahind91.github.io

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Random Name Generator with Images</title>
  <style>
    body { font-family: sans-serif; padding: 2rem; background: #f0f0f0; text-align: center; }
    button { font-size: 1.1rem; padding: 0.7rem 1.2rem; margin: 1rem 0; cursor: pointer; }
    #result { font-size: 1.3rem; margin-top: 1rem; color: #333; }
    img { margin-top: 1rem; max-width: 250px; border-radius: 8px; box-shadow: 0 0 10px rgba(0,0,0,0.2); }
    h1 { color: #222; }
    p { margin: 0.3rem 0; }
  </style>
</head>
<body>
  <h1>Random Name & Breed Generator with Wish Artwork</h1>

  <button onclick="generateName()">Generate Character + Breed + Image</button>
  <div id="result"></div>

  <script>
    // Full list of Genshin characters with model sizes and image URLs from Wish Artworks
    // Image URLs are from the wiki's Wish Gallery, direct links to images
    const genshinCharacters = [
      { name: "Albedo", model: "Medium Male", image: "https://genshin-impact.fandom.com/wiki/File:Albedo_Wish.png" },
      { name: "Alhaitham", model: "Medium Male", image: "https://genshin-impact.fandom.com/wiki/File:Alhaitham_Wish.png" },
      { name: "Aloy", model: "Medium Female", image: "https://genshin-impact.fandom.com/wiki/File:Aloy_Wish.png" },
   
    ];

    // Full horse breeds list (sample subset, add more if needed)
    const horseBreeds = [
      "Abaga", "Abyssinian", "Adaev", "Aegidienberger", "Akhal-Teke",
      "Albanian", "Altai", "Alter Real", "American Bashkir Curly", "American Belgian Draft",
      "American Cream Draft", "American Indian Horse", "American Paint Horse", "American Quarter Horse",
      "American Saddlebred", "American Warmblood", "Andalusian", "Andravida", "Anglo-Arabian",
      "Anglo-Kabarda", "Appaloosa", "Arabian", "Ardennais", "Arenberg-Nordkirchen", "Asturcón",
      "Australian Draught", "Australian Stock Horse", "Austrian Warmblood", "Auvergne", "Auxois",
      "Axios", "Azerbaijan", "Azteca", "Baise horse, Guangxi", "Bale",
      "Balearic horse, see Mallorquín and Menorquín", "Balikun horse", "Baluchi horse", "Banker horse",
      "Barb horse", "Bardigiano", "Bashkir horse", "Basque Mountain Horse", "Bavarian Warmblood",
      "Belgian Draught, also Brabant, Belgisch Trekpaard, Trait belge", "Belgian Sport Horse", "Belgian Trotter",
      "Belgian Warmblood (includes Belgian Half-blood)", "Bhutia Horse, also Bhotia, Bhote ghoda, Bhutan, Bhutani, Bhutua",
      "Black Forest Horse or Black Forest Coldblood", "Blazer horse", "Boerperd", "Borana", "Bosnian Mountain Horse",
      "Boulonnais horse", "Brandenburger", "Brazilian Sport Horse (Brasileiro de Hipismo)", "Breton horse, or Trait Breton",
      "British Warmblood", "Brumby", "Budyonny horse or Budenny", "Burguete horse", "Burmese Horse",
      "Byelorussian Harness Horse", "Calabrese horse", "Camargue horse", "Camarillo White Horse", "Campeiro",
      "Campolina", "Canadian horse", "Canadian Pacer", "Carolina Marsh Tacky", "Carthusian Spanish horse",
      "Caspian horse", "Castilian, see Andalusian", "Castillonnais", "Catria horse", "Cavallo Romano della Maremma Laziale",
      "Cerbat Mustang", "Chickasaw Horse, see Florida Cracker Horse", "Chaidamu horse", "Chakouyi", "Chernomor horse",
      "Chilean horse or Chilean Corralero", "Chinese Mongolian horse", "Choctaw horse", "Cleveland Bay", "Clydesdale horse",
      "Colorado Ranger", "Coldblood trotter", "Comtois horse", "Corsican horse", "Costa Rican Saddle Horse",
      "Cretan horse, see Messara", "Criollo horse", "Croatian Coldblood", "Cuban Criollo", "Cumberland Island horse",
      "Czech Warmblood", "Daliboz, see Azerbaijan horse", "Danish Warmblood", "Danube Delta horse", "Dareshuri",
      "Datong horse", "Dølehest", "Don, see Russian Don", "Dongola horse", "Dutch Harness Horse", "Dutch Draft",
      "Dutch Warmblood", "Dzungarian horse, see Przewalski's horse", "East Bulgarian", "Estonian Draft", "Estonian Native",
      "Ethiopian horses", "Falabella", "Faroese or Faroe horse, see Faroe pony in pony section", "Finnhorse, or Finnish Horse",
      "Flemish Horse", "Fleuve", "Fjord horse, also Norwegian Fjord Horse", "Florida Cracker Horse", "Foutanké or Fouta",
      "Frederiksborger", "Freiberger", "French Trotter", "Friesian", "Furioso-North Star", "Galiceno or Galiceño",
      "Gelderland horse", "Giara Horse", "Gidran", "Groningen Horse", "Hackney horse", "Haflinger", "Hanoverian horse",
      "Heck horse", "Heihe horse", "Henson horse", "Hequ horse", "Hirzai", "Hispano-Bretón", "Hispano-Árabe also known as Hispano or Spanish Anglo-Arab",
      "Holsteiner", "Horro", "Hungarian Warmblood", "Icelandic horse", "Indian Country-bred", "Iomud", "Irish Draught",
      "Irish Sport Horse or Irish Hunter", "Italian Heavy Draft", "Italian Trotter", "Jaca Navarra", "Jeju horse", "Jutland horse",
      "Kabarda horse, also known as Kabardian or Kabardin", "Kafa", "Kaimanawa horses", "Kalmyk horse", "Karabair",
      "Karabakh horse also known as Azer At", "Karossier see Ostfriesen and Alt-Oldenburger", "Karachai horse", "Kathiawari horse",
      "Kazakh Horse", "Kentucky Mountain Saddle Horse", "Kiger Mustang", "Kinsky horse", "Konik", "Kyrgyz Horse",
      "Kisber Felver", "Kiso Horse", "Kladruber", "Knabstrupper", "Kundudo horse", "Kurdish horse", "Kustanair",
      "Latvian horse", "Lipizzan or Lipizzaner", "Lithuanian Heavy Draught", "Ljutomer Trotter", "Lokai", "Losino horse",
      "Lusitano", "Luxembourg Warmblood", "Lyngshest, see Nordlandshest/ Lyngshest", "M'Bayar", "M'Par", "Malopolski",
      "Mallorquín", "Mangalarga", "Mangalarga Marchador", "Marismeño", "Marwari horse", "Messara horse", "Messenger horse",
      "Messenger of the Gods", "Missouri Fox Trotter", "Misaki horse", "Mokara pony", "Mongolian horse", "Morab",
      "Morocco horse", "Mori", "Moscow Mule", "Mustang", "Mvg", "Muzzle horse", "Myron horse", "Nahual horse", "Namyang horse",
      "Navajo horse", "Nez Perce horse", "New Forest pony", "Newfoundland pony", "Newfoundland horse", "Nonius", "Noriker",
      "Norwegian Fjord horse", "North Swedish horse", "Norwich horse", "Nottingham horse", "Nova Scotia Duck Tolling Retriever horse",
      "Nubra horse", "Nyala horse", "Oberlander horse", "Obe horse", "Odenwald horse", "Oldenburg horse", "Oldenburg International",
      "Oldenburg Land horse", "Oldenburg Type horse", "Orlov trotter", "Ossetian horse", "Ostfriesen and Alt-Oldenburger",
      "Överhogdal horse", "Pampa horse", "Paso Fino", "Paso Peruano", "Peneia Pony", "Percheron", "Peruvian Paso", "Persian horse",
      "Pindos horse", "Pinsk horse", "Pony of the Americas", "Posavac horse", "Pottok", "Przewalski's horse", "Pura Raza Española",
      "Pyrenean Horse", "Qatgani horse", "Quarter horse", "Quarab", "Raidi horse", "Raubi horse", "Raum horse", "Red Hare",
      "Rhenish German Coldblood", "Rhenish Warmblood", "Riwoche horse", "Rocky Mountain horse", "Romanian Sport Horse",
      "Rottaler", "Russian Don", "Russian Heavy Draft", "Russian Trotter", "Russian Riding Horse", "Russian Pony",
      "Sable Island horse", "Sakhalin horse", "Saklawi", "Sangamneri", "Sardinian Anglo-Arab", "Sart horse", "Selle Français",
      "Senner horse", "Shetland pony", "Siberian horse", "Silesian horse", "Sokólski horse", "Sorraia horse", "South German Coldblood",
      "Spanish Mustang", "Spanish-Norman horse", "Spanish-Norman horse (PN)",
      "Spiti horse", "Standardbred", "Suffolk Punch", "Sumpter horse", "Svalbard pony", "Swedish Ardennes horse",
      "Swedish Warmblood", "Swiss Warmblood", "Szegediner horse", "Tachyr horse", "Tafjord horse", "Taiwan pony",
      "Tarpan", "Tatarski horse", "Tennessee Walking Horse", "Terceira", "Theresian horse", "Thoroughbred",
      "Timber horse", "Tinker horse", "Tobiano horse", "Tornjak horse", "Tori horse", "Toubou horse", "Transylvanian horse",
      "Trakehner", "Treasure Coast horse", "Trojan horse", "Trotter", "Tulia horse", "Tuvan horse", "Tyrolean Haflinger",
      "Ukrainian Saddle horse", "Uruguayan Criollo", "Uzunyayla", "Vanner horse", "Värmland horse", "Vendeen horse",
      "Vestland horse", "Virginia Highlander", "Vlaamperd", "Vlaamse paard", "Vlaamse paard (Belgian Draft)",
      "Waler horse", "Westphalian horse", "West Swedish horse", "Westfälisches Pferd", "Western horse",
      "Western Sudan horse", "Wielkopolski horse", "Württemberger horse", "Xilingol horse", "Yili horse", "Zangersheide",
      "Zhemaichu", "Zimbru horse", "Zweigelt horse", "Zweibrücker", "Žemaitukas"
    ];



    // Full pony breeds list (sample subset, add more if needed)
    const ponyBreeds = [
      "American Shetland Pony", "American Walking Pony", "Anadolu Pony", "Assateague",
      "Australian Pony", "Australian Riding Pony", "Bali Pony",
      "Basuto pony, also spelled Basotho pony", "Batak Pony", "Bhirum pony",
      "Bosnian Mountain Horse", "British Spotted Pony", "Burmese pony",
      "Camargue horse see horse section", "Canadian rustic pony",
      "Carpathian Pony, see Hucul Pony", "Caspian horse see horse section",
      "Chincoteague Pony", "Chinese Guoxia", "Coffin Bay Pony", "Connemara pony",
      "Czechoslovakian Small Riding Pony", "Dales Pony", "Danish Sport Pony",
      "Dartmoor pony", "Deli pony", "Dülmen Pony", "Eriskay pony", "Esperia Pony",
      "Exmoor pony", "Falabella see horse section", "Faroe pony", "Fell Pony",
      "Flores pony, see Timor Pony", "French Saddle Pony", "Galician Pony",
      "Garrano", "Gayoe", "German Riding Pony, Deutsche Reitpony",
      "German Classic Pony", "Gotland Pony, Skogsruss", "Guizhou pony",
      "Gǔo-xìa pony, see Chinese Guoxia", "Hackney pony", "Haflinger see horse section",
      "Highland pony", "Hokkaido Pony", "Hucul Pony, also called Huțul Pony",
      "Icelandic horse see horse section", "Java Pony", "Karelian pony", "Kerry bog pony",
      "Lac La Croix Indian Pony", "Landais Pony", "Lijiang pony", "Lundy Pony",
      "Manipuri Pony", "Merens Pony, also called Ariegeois pony, see Merens horse",
      "Miniature horse, see horse section", "Miyako Pony", "Namaqua Pony", "Narym Pony",
      "New Forest pony", "Newfoundland pony", "Peneia Pony", "Petiso Argentino",
      "Pindos Pony", "Poney du Logone, also called Poney Mousseye", "Pony of the Americas",
      "Quarter pony", "Sable Island Pony", "Sandalwood Pony", "Shetland pony",
      "Skyros Pony", "Sumba and Sumbawa Pony", "Tibetan Pony", "Timor Pony", "Welara",
      "Welsh Pony (sections A, B and C)", "Western Sudan pony"
    ];

    function generateName() {
      const charIndex = Math.floor(Math.random() * genshinCharacters.length);
      const character = genshinCharacters[charIndex];
      const model = character.model;

      let breed = "";

      if (model.toLowerCase().includes("tall")) {
        breed = horseBreeds[Math.floor(Math.random() * horseBreeds.length)];
      } else if (model.toLowerCase().includes("short")) {
        breed = ponyBreeds[Math.floor(Math.random() * ponyBreeds.length)];
      } else {
        // For medium, pick from all breeds
        const allBreeds = horseBreeds.concat(ponyBreeds);
        breed = allBreeds[Math.floor(Math.random() * allBreeds.length)];
      }

      const resultDiv = document.getElementById("result");
      resultDiv.innerHTML = `
        <p><strong>Character:</strong> ${character.name}</p>
        <img src="${character.image}" alt="${character.name} Wish Artwork" />
        <p><strong>Model:</strong> ${model}</p>
        <p><strong>Breed:</strong> ${breed}</p>
      `;
    }
  </script>
</body>
</html>

