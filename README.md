
<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>নাম ও সংখ্যা তালিকা</title>
  <style>
    body {
      font-family: 'SolaimanLipi', sans-serif;
      background: #f0f8ff;
      padding: 20px;
      max-width: 500px;
      margin: auto;
    }
    h1 {
      text-align: center;
      font-size: 24px;
    }
    input, button {
      padding: 10px;
      margin: 5px 0;
      width: 100%;
      font-size: 16px;
      box-sizing: border-box;
    }
    ul {
      list-style-type: none;
      padding: 0;
    }
    li {
      background: #e0f7fa;
      margin: 5px 0;
      padding: 10px;
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .delete-btn {
      background: red;
      color: white;
      border: none;
      padding: 5px 10px;
      cursor: pointer;
      border-radius: 4px;
    }
    .delete-btn:hover {
      background: darkred;
    }
  </style>
</head>
<body>
  <h1>নাম ও সংখ্যা সংরক্ষণ</h1>
  <input type="text" id="nameInput" placeholder="নাম লিখো">
  <input type="number" id="numberInput" placeholder="সংখ্যা লিখো">
  <button onclick="addEntry()">সংরক্ষণ করো</button>

  <ul id="entryList"></ul>

  <script>
    const nameInput = document.getElementById('nameInput');
    const numberInput = document.getElementById('numberInput');
    const entryList = document.getElementById('entryList');

    function loadEntries() {
      const entries = JSON.parse(localStorage.getItem('entries') || '[]');
      entryList.innerHTML = '';
      entries.forEach((entry, index) => {
        const li = document.createElement('li');
        li.innerHTML = `${entry.name} - ${entry.number} 
          <button class="delete-btn" onclick="deleteEntry(${index})">ডিলিট</button>`;
        entryList.appendChild(li);
      });
    }

    function addEntry() {
      const name = nameInput.value.trim();
      const number = numberInput.value.trim();

      if (name === '' || number === '') {
        alert('দয়া করে নাম ও সংখ্যা উভয়ই পূরণ করো।');
        return;
      }

      const entries = JSON.parse(localStorage.getItem('entries') || '[]');
      entries.push({ name, number });
      localStorage.setItem('entries', JSON.stringify(entries));

      nameInput.value = '';
      numberInput.value = '';
      loadEntries();
    }

    function deleteEntry(index) {
      const entries = JSON.parse(localStorage.getItem('entries') || '[]');
      entries.splice(index, 1);
      localStorage.setItem('entries', JSON.stringify(entries));
      loadEntries();
    }

    window.onload = loadEntries;
  </script>
</body>
</html>
