# 2019 FRQ 4: Light Board

<!-- HTML must be above JS to create result body before JS access -->
<body>
    <h2>Single Light Bulb Info</h2>
    <table>
    <thead>
    <tr>
        <th>Red</th>
        <th>Green</th>
        <th>Blue</th>
        <th>Effect</th>
    </tr>
    </thead>
    <tbody id="result">
        <!-- javascript generated data -->
    </tbody>
    </table>
    <button id="bulb" onclick="getBulbInfo()">Switch bulb!</button>
    <h2>Multiple Light Bulbs Info</h2>
    <table>
    <thead>
    <tr>
        <th>Red</th>
        <th>Green</th>
        <th>Blue</th>
        <th>Effect</th>
    </tr>
    </thead>
    <tbody id="results">
        <!-- javascript generated data -->
    </tbody>
    </table>
    <button id="bulbs" onclick="addBulbInfo()">Add bulb!</button>
</body>

<script>
  // prepare HTML defined containers for new outputs in table
  const resultContainer = document.getElementById("results");
  const bulbInfo = document.getElementById("result");
  const boardInfo = document.getElementById("board");
  const boardWithEffect = document.getElementById("boardWithEffect");

  // match buttons to functions
  const bulb = document.getElementById("bulb");
  bulb.onclick = function() {
    getBulbInfo()
  };
  const bulbs = document.getElementById("bulbs");
  bulbs.onclick = function() {
    addBulbInfo()
  };


  // prepare fetch urls
  const url = "https://rebeccaaa.tk/api/light";
  const get_url = url + "/random";
  const board_url = url + "/board";

  // prepare fetch GET options
  const options = {
    method: 'GET', // *GET, POST, PUT, DELETE, etc.
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'same-origin', // include, same-origin, omit
    headers: {
      'Content-Type': 'application/json'
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
  };

function getBulbInfo(){
  // fetch the API
  fetch(get_url, options)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors
      if (response.status !== 200) {
          error('GET API response failure: ' + response.status);
          return;
      }
      // valid response will have JSON data
      response.json().then(data => {
        console.log(data);
        const tr = document.createElement("tr");
        // td for red
        const red = document.createElement("td");
        red.innerHTML = data.red;

        // td for green
        const green = document.createElement("td");
        green.innerHTML = data.green;

        // td for blue
        const blue = document.createElement("td");
        blue.innerHTML = data.blue;

        // td for effect
        const effect = document.createElement("td");
        effect.innerHTML = data.effect;

        // this builds ALL td's (cells) into tr (row) element
        tr.appendChild(red);
        tr.appendChild(green);
        tr.appendChild(blue);
        tr.appendChild(effect);

        // this adds all the tr (row) work above to the HTML "result" container
        bulbInfo.appendChild(tr);
      })
  })
  // catch fetch errors (ie Nginx ACCESS to server blocked)
  .catch(err => {
    error(err + " " + get_url);
  });
}

function addBulbInfo(){
  // fetch the API
  fetch(get_url, options)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors
      if (response.status !== 200) {
          error('GET API response failure: ' + response.status);
          return;
      }
      // valid response will have JSON data
      response.json().then(data => {
        console.log(data);
        const tr = document.createElement("tr");
        // td for red
        const red = document.createElement("td");
        red.innerHTML = data.red;

        // td for green
        const green = document.createElement("td");
        green.innerHTML = data.green;

        // td for blue
        const blue = document.createElement("td");
        blue.innerHTML = data.blue;

        // td for effect
        const effect = document.createElement("td");
        effect.innerHTML = data.effect;


        // this builds ALL td's (cells) into tr (row) element
        tr.appendChild(red);
        tr.appendChild(green);
        tr.appendChild(blue);
        tr.appendChild(effect);

        // this adds all the tr (row) work above to the HTML "result" container
        resultContainer.appendChild(tr);
      })
  })
  // catch fetch errors (ie Nginx ACCESS to server blocked)
  .catch(err => {
    error(err + " " + get_url);
  });
}

  // Something went wrong with actions or responses
  function error(err) {
    // log as Error in console
    console.error(err);
    // append error to resultContainer
    const tr = document.createElement("tr");
    const td = document.createElement("td");
    td.innerHTML = err;
    tr.appendChild(td);
    resultContainer.appendChild(tr);
  }
</script>