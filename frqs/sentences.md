# Word and Character Counter

<body>
    <h2>Enter text below:</h2>
    <textarea name="paragraph_text" cols="70" rows="10" id="input1"></textarea>
    <button onclick="calculate()">Calculate!</button>
    <h3>Text Entered</h3>
        <p id="txt"></p>
    <h3>Characters (excluding spaces)</h3>
        <p id="char"></p>
    <h3>Characters (including spaces)</h3>
        <p id="charSpace"></p>
    <h3>Words</h3>
        <p id="words"></p>
</body>

<script>
    const url = "https://csa.rebeccaaa.tk/api/sentences/calculate";
    function calculate(){
        var text = document.getElementById('input1').value;
        const options = {
            method: 'POST',
            headers: {
            'Content-Type': 'application/json'
            },
            body: JSON.stringify(text),
        };
        fetch(url, options)
        .then(response => {
        // check for response errors
        if (response.status !== 200) {
            error('GET API response failure: ' + response.status);
            return;
        }
        // valid response will have JSON data
        response.json().then(data => {
            console.log(data);
            document.getElementById("txt").innerHTML = data.Original;
            // subtracting 2 to account for apostrophes
            document.getElementById("char").innerHTML = data.Characters-2;
            document.getElementById("charSpace").innerHTML = data.Spaces-2;
            document.getElementById("words").innerHTML = data.Words;
        });
    })
    // catch fetch errors (ie Nginx ACCESS to server blocked)
    .catch(err => {
        error(err + " " + get_url);
    });
}    

  // Something went wrong with actions or responses
  function error(err) {
    // log as Error in console
    console.error(err);
    document.getElementById("words").innerHTML = err;
  }
</script>