# 2019 FRQ 1: Calender
<script>

function dayOfWeek() {
    var month = document.getElementById("month").value;
    var day = document.getElementById("day").value;
    var year = document.getElementById("year").value;
    var str_url = "https://csa.rebeccaaa.tk/api/calendar/dayOfWeek/" + month + "/" + day + "/" + year;
    console.log(str_url);


  // fetch the API
  fetch(str_url)
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
          console.log(data.dayOfWeek);
          document.getElementById("dayofWeek_number").innerHTML = data.dayOfWeek;
          if (data.dayOfWeek == 0) {
            document.getElementById("sunday").innerHTML = "it is a sunday!";
          } else if (data.dayOfWeek == 1) {
            document.getElementById("monday").innerHTML = "it is a monday!";
          } else if (data.dayOfWeek == 2) {
            document.getElementById("tuesday").innerHTML = "it is a tuesday!";
          }else if (data.dayOfWeek == 3) {
            document.getElementById("wednesday").innerHTML = "it is a wednesday!";
          }else if (data.dayOfWeek == 4) {
            document.getElementById("thursday").innerHTML = "it is a thursday!";
          }else if (data.dayOfWeek == 5) {
            document.getElementById("friday").innerHTML = "it is a friday!";
          }else if (data.dayOfWeek == 6) {
            document.getElementById("saturday").innerHTML = "it is a saturday!";
          }else {
            console.log("something went wrong, no day?");
          }
      })
  })
  // catch fetch errors (ie Nginx ACCESS to server blocked)
  .catch(err => {
    error(err + " " + get_url);
  });

}

</script>

<label for="month">Month:</label>
<input type="text" id="month" name="month" placeholder="mm">

<label for="day">Day:</label>
<input type="text" id="day" name="day" placeholder="dd">

<label for="year">Year:</label>
<input type="text" id="year" name="year" placeholder="yyyy">
<br>

<button onclick="dayOfWeek()">Try it</button>
<br>
<br>
<p id="dayofWeek_number"></p>
<br>
<p id="sunday"></p>
<p id="monday"></p>
<p id="tuesday"></p>
<p id="wednesday"></p>
<p id="thursday"></p>
<p id="friday"></p>
<p id="saturday"></p>

<br>
<br>


