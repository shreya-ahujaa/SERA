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


