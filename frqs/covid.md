# Covid Frontend

<script>
function country(){
    var country_name = document.getElementById("country").value;
    const url = "https://csa.rebeccaaa.tk/api/covid/daily/";
    fetch(url)
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
            for (const row of data.countries_stat) {
                if (country_name = data.countries_stat.country_name){
                    document.getElementById("cases").innerHTML = data.countries_stat.cases;
                }
        
            }



                            
        })
    })

}
</script>




<h2>Enter a country name</h2>
<label for="country">Country:</label>
<input type="text" id="country" name="country" placeholder="Country">
<br>
<button onclick="country()">Go!</button> 
<br>
<h3 id="cases"></h3>
<br>
<br>
 