# Meeting Minutes Database Frontend Guide

 <form>
        <label for="date">Date</label>
        <input type="text" id="date" placeholder="MM/DD/YYYY"/>
        <br>
        <br>
        <label for="person_who_logged">Name of the Person Logging in</label>
        <input type="person_who_logged" id="person_who_logged" placeholder="aadya"/>
        <br>   
        <br>    
        <input type="file" id="myFile" name="filename">
        <br>
        <br>
        <button onclick="minutes()">Submit</button>

</form>

<h3 id="submitted"></h3>


<script>

    function minutes(){
        document.getElementById("submitted").innerHTML = "Input Submitted Successfully!";
    }

</script>