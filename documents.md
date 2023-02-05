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
<center>

<label for="date">Date:</label><br>
<input type="text" id="date" name="date" value="MM/DD/YYYY"><br>
<label for="name">Name:</label><br>
<input type="text" id="name" name="name" value="aadya daita"><br><br>

<textarea id="w3review" name="w3review" rows="4" cols="50">Enter text here</textarea>


<br>
<label for="year_leap">Year:</label>
<input type="text" id="year_leap" name="year_leap" placeholder="##">
<br>
<button onclick="isLeapYear()">Go!</button> 
<br>
<h3 id="isLeapYear_result"></h3>
<br>
<br>

</center>

