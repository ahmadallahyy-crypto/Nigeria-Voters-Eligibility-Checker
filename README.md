<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Nigeria Voters Eligibility Checker</title>
  <style>
    body {
      font-family: Arial, Tahoma, sans-serif;
      padding: 20px;
      background-color: #f0f8ff;
      max-width: 700px;
      margin: 0 auto;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      border-radius: 10px;
    }

    h1 {
      text-align: center;
      color: #008751;
      text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
    }

    .input-group {
      margin-bottom: 15px;
      border: 2px solid #008751;
      border-radius: 8px;
      padding: 15px;
      background-color: white;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }

    label {
      display: block;
      font-weight: bold;
      margin-bottom: 8px;
      color: #333;
    }

    input, select {
      width: 100%;
      padding: 10px;
      border: 1px solid #d3baba;
      border-radius: 4px;
      font-size: 14px;
      box-sizing: border-box;
    }

    button {
      padding: 12px 25px;
      background: linear-gradient(to right, #2f8764, #00a859);
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
      margin-top: 10px;
      width: 100%;
      font-weight: bold;
      transition: background 0.3s;
    }

    button:hover {
      background: linear-gradient(to right, #007544, #008751);
    }

    #result {
      margin-top: 20px;
      padding: 20px;
      border: 2px solid #008751;
      background-color: #f9fff9;
      border-radius: 8px;
      font-size: 16px;
      min-height: 60px;
      display: none;
    }

    .error {
      color: #e74c3c;
      font-weight: bold;
      background-color: #ffeaea;
      padding: 10px;
      border-radius: 4px;
    }

    .success {
      color: #27ae60;
      font-weight: bold;
      background-color: #eafaf1;
      padding: 10px;
      border-radius: 4px;
    }

    .warning {
      color: #f39c12;
      font-weight: bold;
      background-color: #fff8e1;
      padding: 10px;
      border-radius: 4px;
    }

    .info {
      color: #3498db;
      background-color: #e8f4fc;
      padding: 10px;
      border-radius: 4px;
    }

    .form-title {
      text-align: center;
      color: #008751;
      margin-bottom: 20px;
      font-size: 18px;
    }

    .flag {
      text-align: center;
      font-size: 24px;
      margin-bottom: 10px;
    }
  </style>
</head>

<body>

  <div class="flag">🇳🇬</div>
  <h1>Nigeria Voters Eligibility Checker</h1>
  <div class="form-title">INEC Voter Registration Verification System</div>

  <div class="input-group">
    <label for="nameInput">Full Name:</label>
    <input type="text" id="nameInput" placeholder="Enter your full name (as on INEC card)">
  </div>

  <div class="input-group">
    <label for="voterIdInput">Voter Identification Number (VIN):</label>
    <input type="text" id="voterIdInput" placeholder="Enter 19-digit VIN (e.g., 90F5B0123456789ABCD)">
    <small style="color: #666; font-size: 12px; display: block; margin-top: 5px;">VIN is a 19-character alphanumeric code on your Permanent Voter's Card</small>
  </div>

  <div class="input-group">
    <label for="ageInput">Age:</label>
    <input type="number" id="ageInput" value="18" min="0" max="120">
  </div>

  <div class="input-group">
    <label for="stateSelect">State of Origin:</label>
    <select id="stateSelect" onchange="updateLGAs()">
      <option value="">Select State</option>
      <option value="Abia">Abia State</option>
      <option value="Adamawa">Adamawa State</option>
      <option value="Akwa Ibom">Akwa Ibom State</option>
      <option value="Anambra">Anambra State</option>
      <option value="Bauchi">Bauchi State</option>
      <option value="Bayelsa">Bayelsa State</option>
      <option value="Benue">Benue State</option>
      <option value="Borno">Borno State</option>
      <option value="Cross River">Cross River State</option>
      <option value="Delta">Delta State</option>
      <option value="Ebonyi">Ebonyi State</option>
      <option value="Edo">Edo State</option>
      <option value="Ekiti">Ekiti State</option>
      <option value="Enugu">Enugu State</option>
      <option value="FCT">Federal Capital Territory</option>
      <option value="Gombe">Gombe State</option>
      <option value="Imo">Imo State</option>
      <option value="Jigawa">Jigawa State</option>
      <option value="Kaduna">Kaduna State</option>
      <option value="Kano">Kano State</option>
      <option value="Katsina">Katsina State</option>
      <option value="Kebbi">Kebbi State</option>
      <option value="Kogi">Kogi State</option>
      <option value="Kwara">Kwara State</option>
      <option value="Lagos">Lagos State</option>
      <option value="Nasarawa">Nasarawa State</option>
      <option value="Niger">Niger State</option>
      <option value="Ogun">Ogun State</option>
      <option value="Ondo">Ondo State</option>
      <option value="Osun">Osun State</option>
      <option value="Oyo">Oyo State</option>
      <option value="Plateau">Plateau State</option>
      <option value="Rivers">Rivers State</option>
      <option value="Sokoto">Sokoto State</option>
      <option value="Taraba">Taraba State</option>
      <option value="Yobe">Yobe State</option>
      <option value="Zamfara">Zamfara State</option>
    </select>
  </div>

  <div class="input-group">
    <label for="lgaSelect">Local Government Area (LGA):</label>
    <select id="lgaSelect">
      <option value="">Select State First</option>
    </select>
  </div>

  <button onclick="checkEligibility()">Check Voter Eligibility</button>

  <div id="result"></div>

  <script>
    // Nigerian LGAs by State
    const lgasByState = {
      "Abia": ["Aba North", "Aba South", "Arochukwu", "Bende", "Ikwuano", "Isiala Ngwa North", "Isiala Ngwa South", "Isuikwuato", "Obi Ngwa", "Ohafia", "Osisioma", "Ugwunagbo", "Ukwa East", "Ukwa West", "Umuahia North", "Umuahia South", "Umu Nneochi"],
      "Adamawa": ["Demsa", "Fufure", "Ganye", "Gayuk", "Gombi", "Grie", "Hong", "Jada", "Lamurde", "Madagali", "Maiha", "Mayo Belwa", "Michika", "Mubi North", "Mubi South", "Numan", "Shelleng", "Song", "Toungo", "Yola North", "Yola South"],
      "Akwa Ibom": ["Abak", "Eastern Obolo", "Eket", "Esit Eket", "Essien Udim", "Etim Ekpo", "Etinan", "Ibeno", "Ibesikpo Asutan", "Ibiono-Ibom", "Ikot Abasi", "Ikot Ekpene", "Ini", "Itu", "Mbo", "Mkpat-Enin", "Nsit-Atai", "Nsit-Ibom", "Nsit-Ubium", "Obot Akara", "Okobo", "Onna", "Oron", "Oruk Anam", "Udung-Uko", "Ukanafun", "Uruan", "Urue-Offong/Oruko", "Uyo"],
      "Anambra": ["Aguata", "Anambra East", "Anambra West", "Anaocha", "Awka North", "Awka South", "Ayamelum", "Dunukofia", "Ekwusigo", "Idemili North", "Idemili South", "Ihiala", "Njikoka", "Nnewi North", "Nnewi South", "Ogbaru", "Onitsha North", "Onitsha South", "Orumba North", "Orumba South", "Oyi"],
      "Bauchi": ["Alkaleri", "Bauchi", "Bogoro", "Damban", "Darazo", "Dass", "Gamawa", "Ganjuwa", "Giade", "Itas/Gadau", "Jama'are", "Katagum", "Kirfi", "Misau", "Ningi", "Shira", "Tafawa Balewa", "Toro", "Warji", "Zaki"],
      "Bayelsa": ["Brass", "Ekeremor", "Kolokuma/Opokuma", "Nembe", "Ogbia", "Sagbama", "Southern Ijaw", "Yenagoa"],
      "Benue": ["Ado", "Agatu", "Apa", "Buruku", "Gboko", "Guma", "Gwer East", "Gwer West", "Katsina-Ala", "Konshisha", "Kwande", "Logo", "Makurdi", "Obi", "Ogbadibo", "Ohimini", "Oju", "Okpokwu", "Otukpo", "Tarka", "Ukum", "Ushongo", "Vandeikya"],
      "Borno": ["Abadam", "Askira/Uba", "Bama", "Bayo", "Biu", "Chibok", "Damboa", "Dikwa", "Gubio", "Guzamala", "Gwoza", "Hawul", "Jere", "Kaga", "Kala/Balge", "Konduga", "Kukawa", "Kwaya Kusar", "Mafa", "Magumeri", "Maiduguri", "Marte", "Mobbar", "Monguno", "Ngala", "Nganzai", "Shani"],
      "Cross River": ["Abi", "Akamkpa", "Akpabuyo", "Bakassi", "Bekwarra", "Biase", "Boki", "Calabar Municipal", "Calabar South", "Etung", "Ikom", "Obanliku", "Obubra", "Obudu", "Odukpani", "Ogoja", "Yakuur", "Yala"],
      "Delta": ["Aniocha North", "Aniocha South", "Bomadi", "Burutu", "Ethiope East", "Ethiope West", "Ika North East", "Ika South", "Isoko North", "Isoko South", "Ndokwa East", "Ndokwa West", "Okpe", "Oshimili North", "Oshimili South", "Patani", "Sapele", "Udu", "Ughelli North", "Ughelli South", "Ukwuani", "Uvwie", "Warri North", "Warri South", "Warri South West"],
      "Ebonyi": ["Abakaliki", "Afikpo North", "Afikpo South", "Ebonyi", "Ezza North", "Ezza South", "Ikwo", "Ishielu", "Ivo", "Izzi", "Ohaozara", "Ohaukwu", "Onicha"],
      "Edo": ["Akoko-Edo", "Egor", "Esan Central", "Esan North-East", "Esan South-East", "Esan West", "Etsako Central", "Etsako East", "Etsako West", "Igueben", "Ikpoba Okha", "Orhionmwon", "Oredo", "Ovia North-East", "Ovia South-West", "Owan East", "Owan West", "Uhunmwonde"],
      "Ekiti": ["Ado Ekiti", "Efon", "Ekiti East", "Ekiti South-West", "Ekiti West", "Emure", "Gbonyin", "Ido Osi", "Ijero", "Ikere", "Ilejemeje", "Irepodun/Ifelodun", "Ise/Orun", "Moba", "Oye"],
      "Enugu": ["Aninri", "Awgu", "Enugu East", "Enugu North", "Enugu South", "Ezeagu", "Igbo Etiti", "Igbo Eze North", "Igbo Eze South", "Isi Uzo", "Nkanu East", "Nkanu West", "Nsukka", "Oji River", "Udenu", "Udi", "Uzo Uwani"],
      "FCT": ["Abaji", "Bwari", "Gwagwalada", "Kuje", "Kwali", "Municipal Area Council"],
      "Gombe": ["Akko", "Balanga", "Billiri", "Dukku", "Funakaye", "Gombe", "Kaltungo", "Kwami", "Nafada", "Shongom", "Yamaltu/Deba"],
      "Imo": ["Aboh Mbaise", "Ahiazu Mbaise", "Ehime Mbano", "Ezinihitte", "Ideato North", "Ideato South", "Ihitte/Uboma", "Ikeduru", "Isiala Mbano", "Isu", "Mbaitoli", "Ngor Okpala", "Njaba", "Nkwerre", "Nwangele", "Obowo", "Oguta", "Ohaji/Egbema", "Okigwe", "Orlu", "Orsu", "Oru East", "Oru West", "Owerri Municipal", "Owerri North", "Owerri West", "Unuimo"],
      "Jigawa": ["Auyo", "Babura", "Biriniwa", "Birnin Kudu", "Buji", "Dutse", "Gagarawa", "Garki", "Gumel", "Guri", "Gwaram", "Gwiwa", "Hadejia", "Jahun", "Kafin Hausa", "Kazaure", "Kiri Kasama", "Kiyawa", "Kaugama", "Maigatari", "Malam Madori", "Miga", "Ringim", "Roni", "Sule Tankarkar", "Taura", "Yankwashi"],
      "Kaduna": ["Birnin Gwari", "Chikun", "Giwa", "Igabi", "Ikara", "Jaba", "Jema'a", "Kachia", "Kaduna North", "Kaduna South", "Kagarko", "Kajuru", "Kaura", "Kauru", "Kubau", "Kudan", "Lere", "Makarfi", "Sabon Gari", "Sanga", "Soba", "Zangon Kataf", "Zaria"],
      "Kano": ["Ajingi", "Albasu", "Bagwai", "Bebeji", "Bichi", "Bunkure", "Dala", "Dambatta", "Dawakin Kudu", "Dawakin Tofa", "Doguwa", "Fagge", "Gabasawa", "Garko", "Garun Mallam", "Gaya", "Gezawa", "Gwale", "Gwarzo", "Kabo", "Kano Municipal", "Karaye", "Kibiya", "Kiru", "Kumbotso", "Kunchi", "Kura", "Madobi", "Makoda", "Minjibir", "Nasarawa", "Rano", "Rimin Gado", "Rogo", "Shanono", "Sumaila", "Takai", "Tarauni", "Tofa", "Tsanyawa", "Tudun Wada", "Ungogo", "Warawa", "Wudil"],
      "Katsina": ["Bakori", "Batagarawa", "Batsari", "Baure", "Bindawa", "Charanchi", "Dandume", "Danja", "Dan Musa", "Daura", "Dutsi", "Dutsin Ma", "Faskari", "Funtua", "Ingawa", "Jibia", "Kafur", "Kaita", "Kankara", "Kankia", "Katsina", "Kurfi", "Kusada", "Mai'Adua", "Malumfashi", "Mani", "Mashi", "Matazu", "Musawa", "Rimi", "Sabuwa", "Safana", "Sandamu", "Zango"],
      "Kebbi": ["Aleiro", "Arewa Dandi", "Argungu", "Augie", "Bagudo", "Birnin Kebbi", "Bunza", "Dandi", "Fakai", "Gwandu", "Jega", "Kalgo", "Koko/Besse", "Maiyama", "Ngaski", "Sakaba", "Shanga", "Suru", "Danko/Wasagu", "Yauri", "Zuru"],
      "Kogi": ["Adavi", "Ajaokuta", "Ankpa", "Bassa", "Dekina", "Ibaji", "Idah", "Igalamela Odolu", "Ijumu", "Kabba/Bunu", "Kogi", "Lokoja", "Mopa Muro", "Ofu", "Ogori/Magongo", "Okehi", "Okene", "Olamaboro", "Omala", "Yagba East", "Yagba West"],
      "Kwara": ["Asa", "Baruten", "Edu", "Ekiti", "Ifelodun", "Ilorin East", "Ilorin South", "Ilorin West", "Irepodun", "Isin", "Kaiama", "Moro", "Offa", "Oke Ero", "Oyun", "Pategi"],
      "Lagos": ["Agege", "Ajeromi-Ifelodun", "Alimosho", "Amuwo-Odofin", "Apapa", "Badagry", "Epe", "Eti Osa", "Ibeju-Lekki", "Ifako-Ijaiye", "Ikeja", "Ikorodu", "Kosofe", "Lagos Island", "Lagos Mainland", "Mushin", "Ojo", "Oshodi-Isolo", "Shomolu", "Surulere"],
      "Nasarawa": ["Akwanga", "Awe", "Doma", "Karu", "Keana", "Keffi", "Kokona", "Lafia", "Nasarawa", "Nasarawa Egon", "Obi", "Toto", "Wamba"],
      "Niger": ["Agaie", "Agwara", "Bida", "Borgu", "Bosso", "Chanchaga", "Edati", "Gbako", "Gurara", "Katcha", "Kontagora", "Lapai", "Lavun", "Magama", "Mariga", "Mashegu", "Mokwa", "Moya", "Paikoro", "Rafi", "Rijau", "Shiroro", "Suleja", "Tafa", "Wushishi"],
      "Ogun": ["Abeokuta North", "Abeokuta South", "Ado-Odo/Ota", "Egbado North", "Egbado South", "Ewekoro", "Ifo", "Ijebu East", "Ijebu North", "Ijebu North East", "Ijebu Ode", "Ikenne", "Imeko Afon", "Ipokia", "Obafemi Owode", "Odeda", "Odogbolu", "Ogun Waterside", "Remo North", "Shagamu"],
      "Ondo": ["Akoko North-East", "Akoko North-West", "Akoko South-East", "Akoko South-West", "Akure North", "Akure South", "Ese Odo", "Idanre", "Ifedore", "Ilaje", "Ile Oluji/Okeigbo", "Irele", "Odigbo", "Okitipupa", "Ondo East", "Ondo West", "Ose", "Owo"],
      "Osun": ["Aiyedire", "Atakunmosa East", "Atakunmosa West", "Ayedaade", "Ayedire", "Boluwaduro", "Boripe", "Ede North", "Ede South", "Egbedore", "Ejigbo", "Ife Central", "Ife East", "Ife North", "Ife South", "Ifedayo", "Ifelodun", "Ila", "Ilesa East", "Ilesa West", "Irepodun", "Irewole", "Isokan", "Iwo", "Obokun", "Odo Otin", "Ola Oluwa", "Olorunda", "Oriade", "Orolu", "Osogbo"],
      "Oyo": ["Afijio", "Akinyele", "Atiba", "Atisbo", "Egbeda", "Ibadan North", "Ibadan North-East", "Ibadan North-West", "Ibadan South-East", "Ibadan South-West", "Ibarapa Central", "Ibarapa East", "Ibarapa North", "Ido", "Irepo", "Iseyin", "Itesiwaju", "Iwajowa", "Kajola", "Lagelu", "Ogbomosho North", "Ogbomosho South", "Ogo Oluwa", "Olorunsogo", "Oluyole", "Ona Ara", "Orelope", "Ori Ire", "Oyo East", "Oyo West", "Saki East", "Saki West", "Surulere"],
      "Plateau": ["Bokkos", "Barkin Ladi", "Bassa", "Jos East", "Jos North", "Jos South", "Kanam", "Kanke", "Langtang North", "Langtang South", "Mangu", "Mikang", "Pankshin", "Qua'an Pan", "Riyom", "Shendam", "Wase"],
      "Rivers": ["Abua/Odual", "Ahoada East", "Ahoada West", "Akuku-Toru", "Andoni", "Asari-Toru", "Bonny", "Degema", "Eleme", "Emuoha", "Etche", "Gokana", "Ikwerre", "Khana", "Obio/Akpor", "Ogba/Egbema/Ndoni", "Ogu/Bolo", "Okrika", "Omuma", "Opobo/Nkoro", "Oyigbo", "Port Harcourt", "Tai"],
      "Sokoto": ["Binji", "Bodinga", "Dange Shuni", "Gada", "Goronyo", "Gudu", "Gwadabawa", "Illela", "Isa", "Kebbe", "Kware", "Rabah", "Sabon Birni", "Shagari", "Silame", "Sokoto North", "Sokoto South", "Tambuwal", "Tangaza", "Tureta", "Wamako", "Wurno", "Yabo"],
      "Taraba": ["Ardo Kola", "Bali", "Donga", "Gashaka", "Gassol", "Ibi", "Jalingo", "Karim Lamido", "Kurmi", "Lau", "Sardauna", "Takum", "Ussa", "Wukari", "Yorro", "Zing"],
      "Yobe": ["Bade", "Bursari", "Damaturu", "Fika", "Fune", "Geidam", "Gujba", "Gulani", "Jakusko", "Karasuwa", "Machina", "Nangere", "Nguru", "Potiskum", "Tarmuwa", "Yunusari", "Yusufari"],
      "Zamfara": ["Anka", "Bakura", "Birnin Magaji/Kiyaw", "Bukkuyum", "Bungudu", "Gummi", "Gusau", "Kaura Namoda", "Maradun", "Maru", "Shinkafi", "Talata Mafara", "Chafe", "Zurmi"]
    };

    function updateLGAs() {
      const stateSelect = document.getElementById("stateSelect");
      const lgaSelect = document.getElementById("lgaSelect");
      const selectedState = stateSelect.value;
      
      // Clear existing options
      lgaSelect.innerHTML = '<option value="">Select LGA</option>';
      
      if (selectedState && lgasByState[selectedState]) {
        // Add LGAs for selected state
        lgasByState[selectedState].forEach(lga => {
          const option = document.createElement("option");
          option.value = lga;
          option.textContent = lga;
          lgaSelect.appendChild(option);
        });
      }
    }

    function validateVIN(vin) {
      // Nigerian VIN is 19 alphanumeric characters
      const vinRegex = /^[A-Z0-9]{19}$/;
      return vinRegex.test(vin);
    }

    function checkEligibility() {
      // Get all input values
      const name = document.getElementById("nameInput").value.trim();
      const voterId = document.getElementById("voterIdInput").value.trim().toUpperCase();
      const age = parseInt(document.getElementById("ageInput").value);
      const state = document.getElementById("stateSelect").value;
      const lga = document.getElementById("lgaSelect").value;
      
      const resultDiv = document.getElementById("result");
      resultDiv.style.display = "block";
      
      // Validate all inputs
      if (!name) {
        resultDiv.innerHTML = '<span class="error">❌ Please enter your full name as it appears on your INEC card</span>';
        return;
      }
      
      if (!validateVIN(voterId)) {
        resultDiv.innerHTML = '<span class="error">❌ Invalid Voter Identification Number (VIN)<br>Please enter a valid 19-character alphanumeric VIN from your Permanent Voter\'s Card</span>';
        return;
      }
      
      if (isNaN(age) || age < 0) {
        resultDiv.innerHTML = '<span class="error">❌ Please enter a valid age</span>';
        return;
      }
      
      if (!state) {
        resultDiv.innerHTML = '<span class="error">❌ Please select your state of origin</span>';
        return;
      }
      
      if (!lga) {
        resultDiv.innerHTML = '<span class="error">❌ Please select your Local Government Area</span>';
        return;
      }
      
      // Check eligibility
      let message = "";
      const votingAge = 18; // Voting age in Nigeria
      
      if (age < votingAge) {
        message = `<span class="warning">⏳ <strong>Dear ${name},</strong><br><br>
                   VIN: <strong>${voterId}</strong><br>
                   State: <strong>${state}</strong> | LGA: <strong>${lga}</strong><br><br>
                   ❌ <strong>NOT ELIGIBLE TO VOTE</strong><br>
                   You are <strong>${age} years old</strong>.<br>
                   According to Nigerian Constitution, you must be <strong>18 years or older</strong> to vote.<br>
                   You will be eligible to register as a voter in <strong>${votingAge - age} year(s)</strong>.</span>`;
      } else {
        message = `<span class="success">✅ <strong>Dear ${name},</strong><br><br>
                   VIN: <strong>${voterId}</strong><br>
                   State: <strong>${state}</strong> | LGA: <strong>${lga}</strong><br><br>
                   🎉 <strong>ELIGIBLE TO VOTE!</strong><br>
                   You are <strong>${age} years old</strong>.<br>
                   You meet the age requirement for voting in Nigeria.<br>
                   <strong>Remember to bring your PVC to the polling unit.</strong><br><br>
                   <span class="info">📌 <em>Ensure your PVC is not damaged and your details are correct.</em></span></span>`;
      }
      
      resultDiv.innerHTML = message;
    }

    // Add enter key support
    document.addEventListener('keypress', function(event) {
      if (event.key === 'Enter') {
        checkEligibility();
      }
    });

    // Initialize LGA dropdown when state is selected on page load
    document.getElementById('stateSelect').addEventListener('change', updateLGAs);
  </script>

</body>
</html>
