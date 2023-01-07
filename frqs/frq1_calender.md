# 2019 FRQ 1: Calender


<script>
function numberOfLeapYears(){
    var year1 = document.getElementById("year1").value;
    var year2 = document.getElementById("year1").value;
    var str_url_numberOfLeapYears = "https://csa.rebeccaaa.tk/api/calendar/numberOfLeapYears/" + year1 + "/" + year2;

     fetch(str_url_numberOfLeapYears)
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
          console.log(data.numberOfLeapYears);
          document.getElementById("numberOfLeapYears").innerHTML = "there are " + data.numberOfLeapYears + "leap years in between!" ;
      })
  })
  // catch fetch errors (ie Nginx ACCESS to server blocked)
  .catch(err => {
    error(err + " " + get_url);
  });


}




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
    var str_url_dayOfWeek = "https://csa.rebeccaaa.tk/api/calendar/dayOfWeek/" + month + "/" + day + "/" + year;
    console.log(str_url);


  // fetch the API
  fetch(str_url_dayOfWeek)
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
<h2>How many leap years are there between two given years?</h2>
<label for="year1">Year 1:</label>
<input type="text" id="year1" name="year1" placeholder="yyyy">

<label for="year2">Year 2:</label>
<input type="text" id="year2" name="year2" placeholder="yyyy">
<button onclick="numberOfLeapYears()">Try it</button>
<br>
<h2 id="numberOfLeapYears"></h2>
<br>
<br>


<h2>What day of the week is it?</h2>
<label for="month">Month:</label>
<input type="text" id="month" name="month" placeholder="mm">

<label for="day">Day:</label>
<input type="text" id="day" name="day" placeholder="dd">

<label for="year">Year:</label>
<input type="text" id="year" name="year" placeholder="yyyy">
<br>

<button onclick="dayOfWeek()">Try it</button>

<br>
<h3 id="dayofWeek_number"></h3>
<h3 id="sunday"></h3>
<h3 id="monday"></h3>
<h3 id="tuesday"></h3>
<h3 id="wednesday"></h3>
<h3 id="thursday"></h3>
<h3 id="friday"></h3>
<h3 id="saturday"></h3>
<br>
<br>


