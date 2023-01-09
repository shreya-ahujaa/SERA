# 2019 FRQ 3: Calculator

<script>

function calculate(){
    var expression = document.getElementById("expression").value;

    var str_url_expression = "https://csa.rebeccaaa.tk/api/calculator/calculate/" + expression;
    console.log(str_url_expression)

    fetch(str_url_expression)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors
    if (response.status !== 200) {
        error('GET API/Fetch Response Failure: ' + response.status);
        return;
    }
    
    // valid response will have JSON data
    response.json().then(data => {
        console.log(data);
        console.log(data.result);
        document.getElementById("calculated_result").innerHTML = "Result: " + data.result;
    })
})

}

</script>

<br>
<h2>Calculate: </h2>
<label for="expression">Enter Expression: </label>
<input type="text" id="expression" name="expression" >
<br>
<button onclick="calculate()">Calculate!</button> 
<br>
<h3 id="calculated_result">Result: </h3>
<br>
<br>

