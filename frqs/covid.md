# Covid Frontend

<script>
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
      })
  })


</script>