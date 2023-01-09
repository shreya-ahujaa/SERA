# 2019 FRQ 2: Steps


<script>

    
function dailySteps(){
    var total_steps = document.getElementById("total_steps").value;

    var str_url_dailySteps = "https://csa.rebeccaaa.tk/api/step/dailySteps/" + total_steps;
    console.log(str_url_dailySteps)

     fetch(str_url_dailySteps)
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
          console.log(data.dailySteps);
          document.getElementById("dailySteps").innerHTML = "enough? " +  data.dailySteps;
        })
    }) 
}

</script>

<br>
<h2>Enough daily steps?</h2>
<label for="total_steps">Steps:</label>
<input type="text" id="total_steps" name="total_steps" placeholder="####">
<br>
<button onclick="dailySteps()">Go!</button> 
<br>
<h3 id="dailySteps_result"></h3>
<br>
<br>