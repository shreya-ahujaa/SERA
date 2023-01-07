# 2019 FRQ 1: Calender
<script>

function dayOfWeek() {

    document.getElementById("sunday").innerHTML = " ";
    document.getElementById("monday").innerHTML = " ";
    document.getElementById("tuesday").innerHTML = " ";
    document.getElementById("wednesday").innerHTML = " ";
    document.getElementById("thursday").innerHTML = " ";
    document.getElementById("friday").innerHTML = " ";
    document.getElementById("saturday").innerHTML = " ";


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
<h3 id="dayofWeek_number"></h3>
<h1 id="sunday"></h1>
<h1 id="monday"></h1>
<h1 id="tuesday"></h1>
<h1 id="wednesday"></h1>
<h1 id="thursday"></h1>
<h1 id="friday"></h1>
<h1 id="saturday"></h1>

<br>
<br>


