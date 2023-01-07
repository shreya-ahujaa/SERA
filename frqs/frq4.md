# 2019 FRQ 4: Light Board

<head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
</head>
<!-- HTML must be above JS to create result body before JS access -->
<body>
    <h2>Single Light Bulb Info</h2>
    <table id="table">
    <thead>
    <tr>
        <th>Red</th>
        <th>Green</th>
        <th>Blue</th>
        <th>Effect</th>
        <th>Bulb</th>
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
        <th>Bulb</th>
    </tr>
    </thead>
    <tbody id="results">
        <!-- javascript generated data -->
    </tbody>
    </table>
    <button id="bulbs" onclick="addBulbInfo()">Add bulb!</button>
    <h2>Random Light Board (Colors Only)</h2>
    <table>
    <tbody id="board">
    </tbody>
    </table>
    <h2>Random Light Board (Effects: Crossed Out, Italic, Underline, Bold, Faint)</h2>
    <table>
    <tbody id="boardWithEffect">
    </tbody>
    </table>
    <!-- Custom sizing -->
    <h2>Gradient</h2>
    <table>
    <tbody id="gradient2">
    </tbody>
    </table>
    <button onclick="setGradient2()">Create red gradient!</button>
    <table>
    <tbody id="gradient3">
    </tbody>
    </table>
    <button onclick="setGradient3()">Create green gradient!</button>
    <table>
    <tbody id="gradient">
    </tbody>
    </table>
    <button onclick="setGradient()">Create blue gradient!</button>
</body>

<script>
  // prepare HTML defined containers for new outputs in table
  const resultContainer = document.getElementById("results");
  var bulbInfo = document.getElementById("result");
  const boardInfo = document.getElementById("board");
  const boardWithEffect = document.getElementById("boardWithEffect");
  const gradient = document.getElementById("gradient");
  const gradient2 = document.getElementById("gradient2");
  const gradient3 = document.getElementById("gradient3");

  // prepare fetch urls
  const url = "https://rebeccaaa.tk/api/light";
  const get_url = url + "/random";
  const board_url = url + "/board";

  // Modify CSS for bulb effects
  function showBulb(eff, cell){
    cell.style.backgroundColor = "rgb(" + eff.red + ", " + eff.green + ", " + eff.blue + ")";
    if(eff.effect == "Crossed_out"){
      cell.innerHTML = "SLASH SLASH SLASH";
      cell.style.textDecoration = "line-through";
    }
    else if(eff.effect == "Italic"){
      cell.innerHTML = "Italic";
      cell.style.fontStyle = "italic";
    }
    else if(eff.effect == "Underline"){
      cell.innerHTML = "Underline";
      cell.style.textDecoration = "underline";
    }
    else if(eff.effect == "Bold"){
      cell.innerHTML = "Bold";
      cell.style.fontWeight = "bolder";
    }
    else if(eff.effect == "Faint"){
      cell.innerHTML = "Faint";
      cell.style.opacity = "0.3";
    }
    // else if(data[index].light.effect == "Conceal"){
            //   boxEffect.innerHTML = "Conceal";
            //   boxEffect.setAttribute("id", "conceal");
            //   $(document).ready(function() {
            //     $("conceal").hover(
            //       function() {
            //         $(this).css("background-color", "black");
            //       }, 
            //     );
            //   });
            // }
  }

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
        tr.setAttribute("id","row1");
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

        var singleBulbCell = document.createElement("td");
        showBulb(data, singleBulbCell);

        // this builds ALL td's (cells) into tr (row) element
        tr.appendChild(red);
        tr.appendChild(green);
        tr.appendChild(blue);
        tr.appendChild(effect);
        tr.appendChild(singleBulbCell);

        // this adds all the tr (row) work above to the HTML "result" container
        if(document.getElementById("table").rows.length == 2){ // check if row exists
          document.getElementById("table").deleteRow(1);
        }
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

        var bulbCell = document.createElement("td");
        showBulb(data, bulbCell);

        // this builds ALL td's (cells) into tr (row) element
        tr.appendChild(red);
        tr.appendChild(green);
        tr.appendChild(blue);
        tr.appendChild(effect);
        tr.appendChild(bulbCell);

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

  // fetch the API for multiple lights (light board)
  fetch(board_url, options)
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
        var index = 0;
        for (let row = 0; row < 10; row++){ // rows of board
          var tr = document.createElement("tr");
          var trEffect = document.createElement("tr"); // columns of board
          for (let col = 0; col < 10; col++){
            var box = document.createElement("td");
            boxEffect = document.createElement("td");
            box.style.backgroundColor = "rgb(" + data[index].light.red + ", " + data[index].light.green + ", " + data[index].light.blue + ")";
            showBulb(data[index].light, boxEffect);
            tr.appendChild(box);
            trEffect.appendChild(boxEffect);
            index++; // iterating through list of JSON
          }
          board.appendChild(tr);
          boardWithEffect.appendChild(trEffect);
        }
        })
      })  
  // catch fetch errors (ie Nginx ACCESS to server blocked)
  .catch(err => {
    error(err + " " + get_url);
  });

  function setGradient2(){
    var r = 253;
    var g = 29;
    var b = 29;
    for (let row = 0; row < 10; row++){
        var line = document.createElement("tr");
        for (let col = 0; col < 10; col++){
            var cell = document.createElement("td");
            cell.style.backgroundColor = "rgb(" + r + ", " + g + ", " + b + ")";
            line.appendChild(cell);
        }    
        g+=20;
        b-=10;
        gradient2.appendChild(line);
    }
  }

  function setGradient(){
    var r = 0;
    var g = 0;
    var b = 255;
    for (let row = 0; row < 10; row++){
        var line = document.createElement("tr");
        for (let col = 0; col < 10; col++){
            var cell = document.createElement("td");
            cell.style.backgroundColor = "rgb(" + r + ", " + g + ", " + b + ")";
            line.appendChild(cell);
        }    
        r+=20;
        g+=20;
        gradient.appendChild(line);
    }
  }

  function setGradient3(){
    var r = 130;
    var g = 255;
    var b = 127;
    for (let row = 0; row < 10; row++){
        var line = document.createElement("tr");
        for (let col = 0; col < 10; col++){
            var cell = document.createElement("td");
            cell.style.backgroundColor = "rgb(" + r + ", " + g + ", " + b + ")";
            line.appendChild(cell);
        }    
        r-=10;
        g-=20;
        b-=10;
        gradient3.appendChild(line);
    }
  }
</script>
<!-- <style>
    #conceal:hover {
        background-color: black;
    }
</style> -->