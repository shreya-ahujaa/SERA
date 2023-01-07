# 2019 FRQ 1: Calender
<script>

function dayOfWeek() {
    var month = document.getElementById("month").value;
    var day = document.getElementById("day").value;
    var year = document.getElementById("year").value;
    var str_url = "/dayOfWeek/" + month + "/" + day + "/" + year;
    console.log(str_url);
    return str_url; 

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


