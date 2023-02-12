<html>
<br>
<h1> Meeting Documents Database </h1>

<!--

<style>
body {
  background: hsl(220deg, 10%, 97%);
  margin: 0;
  padding: 0;
}

.buttons-container {
  width: 100%;
  height: 40vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

button {
  background: white;
  border: solid 2px black;
  padding: .375em 1.125em;
  font-size: 1rem;
}

.button-arounder {
  font-size: 3rem;
  background: hsl(190deg, 30%, 15%);
  color: hsl(190deg, 10%, 95%);
  
  box-shadow: 0 0px 0px hsla(190deg, 15%, 5%, .2);
  transfrom: translateY(0);
  border-top-left-radius: 0px;
  border-top-right-radius: 0px;
  border-bottom-left-radius: 0px;
  border-bottom-right-radius: 0px;
  
  --dur: .15s;
  --delay: .15s;
  --radius: 16px;
  
 transition:
    border-top-left-radius var(--dur) var(--delay) 
    ease-out,
    border-top-right-radius var(--dur) calc(var(--delay) * 2) ease-out,
    border-bottom-right-radius var(--dur) calc(var(--delay) * 3) 
    ease-out,
    border-bottom-left-radius var(--dur) calc(var(--delay) * 4) 
    ease-out,
    box-shadow calc(var(--dur) * 4) 
    ease-out,
    transform calc(var(--dur) * 4) 
    ease-out,
    background calc(var(--dur) * 4) steps(4, jump-end);
}


.button-arounder:hover,
.button-arounder:focus {
  box-shadow: 0 4px 8px hsla(190deg, 15%, 5%, .2);
  transform: translateY(-4px);
  background: hsl(230deg, 50%, 45%);
  border-top-left-radius: var(--radius);
  border-top-right-radius: var(--radius);
  border-bottom-left-radius: var(--radius);
  border-bottom-right-radius: var(--radius);
}

</style>
-->
<script>

//is leap year code

function documents(){
    var id = document.getElementById("id").value;
    var str_url = "https://csa.rebeccaaa.tk/api/note/" + id;
    console.log(str_url)
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
          console.log(data.document);
          document.getElementById("document_result").innerHTML = "Documents: " +  data.document;
      })
  })

}


</script>


<!--
<label for="date">Date:</label><br>
<input type="text" id="date" name="date" value="MM/DD/YYYY"  maxlength="10" size="4"><br>
-->
<label for="id">Club ID:</label><br>
<input type="text" id="id" name="id" value="##"  maxlength="10" size="4"><br><br>


<!--
<label for="name">Name:</label><br>
<input type="text" id="name" name="name" value="aadya daita"  maxlength="10" size="4"><br><br>

<textarea id="w3review" name="w3review" rows="4" cols="50">Enter text here</textarea>
-->
<button onclick="documents()">Go!</button>

<!--
<div class="buttons-container">
  <button class="button-arounder" >Submit (hover)</button>
</div>
<br>
<h3 id="document_result"></h3>
<br>
<br>

-->