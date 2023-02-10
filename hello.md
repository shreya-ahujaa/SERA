<script>
     // prepare fetch GET options
    const options = {
        method: 'GET', // *GET, POST, PUT, DELETE, etc.
        // mode: 'cors', // no-cors, *cors, same-origin
        cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
        // credentials: 'same-origin', // include, same-origin, omit
        headers: {
        'Content-Type': 'application/json'
        // 'Content-Type': 'application/x-www-form-urlencoded',
        },
    };
    fetch("https://rebeccaaa.tk/hello", options)
    // fetch("https://rebeccaaa.tk/json", options)
    // fetch("http://localhost:8192/hello", options)
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
        document.getElementById("hello").innerHTML = data.json;
        })
    });
    // Something went wrong with actions or responses
    function error(err) {
        // log as Error in console
        console.log(err);
    }
</script>
<h1 id="hello"></h1>
