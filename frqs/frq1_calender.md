# 2019 FRQ 1: Calender


<script>

//is leap year code

function isLeapYear(){

    document.getElementById("sunday_year_firstday").innerHTML = " ";
    document.getElementById("monday_year_firstday").innerHTML = " ";
    document.getElementById("tuesday_year_firstday").innerHTML = " ";
    document.getElementById("wednesday_year_firstday").innerHTML = " ";
    document.getElementById("thursday_year_firstday").innerHTML = " ";
    document.getElementById("friday_year_firstday").innerHTML = " ";
    document.getElementById("saturday_year_firstday").innerHTML = " ";

    var year_leap = document.getElementById("year_leap").value;

    var str_url_isLeapYear = "https://csa.rebeccaaa.tk/api/calendar/isLeapYear/" + year_leap;
    console.log(str_url_isLeapYear)

     fetch(str_url_isLeapYear)
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
          console.log(data.isLeapYear);
          document.getElementById("isLeapYear_result").innerHTML = "leap year? " +  data.isLeapYear;
      })
  })

}




// first day of the year code

function firstDayOfYear(){
    var year_firstday = document.getElementById("year_firstday").value;
    var str_url_year_firstday = "https://csa.rebeccaaa.tk/api/calendar/firstDayOfYear/" + year_firstday;
    console.log(str_url_year_firstday)

     fetch(str_url_year_firstday)
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
          console.log(data.firstDayOfYear);
          document.getElementById("firstDayOfYear").innerHTML = data.firstDayOfYear;
          if (data.firstDayOfYear == 0) {
            document.getElementById("sunday_year_firstday").innerHTML = "it is a sunday!";
          } else if (data.firstDayOfYear == 1) {
            document.getElementById("monday_year_firstday").innerHTML = "it is a monday!";
          } else if (data.firstDayOfYear == 2) {
            document.getElementById("tuesday_year_firstday").innerHTML = "it is a tuesday!";
          }else if (data.firstDayOfYear == 3) {
            document.getElementById("wednesday_year_firstday").innerHTML = "it is a wednesday!";
          }else if (data.firstDayOfYear == 4) {
            document.getElementById("thursday_year_firstday").innerHTML = "it is a thursday!";
          }else if (data.firstDayOfYear == 5) {
            document.getElementById("friday_year_firstday").innerHTML = "it is a friday!";
          }else if (data.firstDayOfYear == 6) {
            document.getElementById("saturday_year_firstday").innerHTML = "it is a saturday!";
          }else {
            console.log("something went wrong, no day?");
          }
      })
  })
}


// how many leap years are in between?

function numberOfLeapYears(){
    var year1 = document.getElementById("year1").value;
    var year2 = document.getElementById("year2").value;
    var str_url_numberOfLeapYears = "https://csa.rebeccaaa.tk/api/calendar/numberOfLeapYears/" + year1 + "/" + year2;
    console.log(str_url_numberOfLeapYears)

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
          document.getElementById("numberOfLeapYears").innerHTML = "there are " + data.numberOfLeapYears + " leap years in between!" ;
      })
  })



}


//what day of the week is it?

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

<br>
<h2>Is it a leap year?</h2>
<label for="year_leap">Year:</label>
<input type="text" id="year_leap" name="year_leap" placeholder="yyyy">
<br>
<button onclick="isLeapYear()">Go!</button> 
<br>
<h3 id="isLeapYear_result"></h3>
<br>
<br>


<h2>What day is the first day of the given year?</h2>
<label for="year_firstday">Year:</label>
<input type="text" id="year_firstday" name="year_firstday" placeholder="yyyy">
<br>
<button onclick="firstDayOfYear()">Go!</button>
<br>
<h3 id="firstDayOfYear"></h3>
<h3 id="sunday_year_firstday"></h3>
<h3 id="monday_year_firstday"></h3>
<h3 id="tuesday_year_firstday"></h3>
<h3 id="wednesday_year_firstday"></h3>
<h3 id="thursday_year_firstday"></h3>
<h3 id="friday_year_firstday"></h3>
<h3 id="saturday_year_firstday"></h3>
<br>
<br>

<h2>How many leap years are there between two given years?</h2>
<label for="year1">Year 1:</label>
<input type="text" id="year1" name="year1" placeholder="yyyy">

<label for="year2">Year 2:</label>
<input type="text" id="year2" name="year2" placeholder="yyyy">
<button onclick="numberOfLeapYears()">Go!</button>
<br>
<h3 id="numberOfLeapYears"></h3>
<br>
<br>


<h2>What day of the week is it given a date?</h2>
<label for="month">Month:</label>
<input type="text" id="month" name="month" placeholder="mm">

<label for="day">Day:</label>
<input type="text" id="day" name="day" placeholder="dd">

<label for="year">Year:</label>
<input type="text" id="year" name="year" placeholder="yyyy">
<br>

<button onclick="dayOfWeek()">Go!</button>

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


