# Meeting Documents Database


<script>

//is leap year code

function isLeapYear(){
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

</script>


  <label for="fname">Date:</label><br>
  <input type="text" id="fname" name="fname" value="MM/DD/YYYY"><br>
  <label for="lname">Name:</label><br>
  <input type="text" id="lname" name="lname" value="aadya daita"><br>
  <br>

<button onclick="isLeapYear()">Go!</button> 
<br>
<h3 id="isLeapYear_result"></h3>
<br>
<br>


