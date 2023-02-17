<html>
<br>
<center> <h1> Meeting Documents Database </h1><center>



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
<script>

function documents(){
    var id = document.getElementById("id").value;
    var str_url = "http://localhost:8192/api/note/" + id;
    console.log(str_url);
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
          for (const row of data) {
            document.getElementById("document_result").innerHTML = "Documents: " +  row.text;
      
          }
      })
  })

}

    function signup2(){
                // get user input
                var text = document.getElementById("text").value;
                var id = document.getElementById("id").value;
                const signup_url = "http://localhost:8192/api/note/post/" + id;
              
                // confirm requirements, matchin
                // store data in JavaScript object
                let data = {id: id, text: text};
                console.log(data);
                const options = {
                    method: 'POST',
                    mode: 'cors',
                    cache: 'no-cache',
                    credentials: 'include',
                    headers: {
                    'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(data), // convert to JSON
                };
                fetch(signup_url, options)
                .then(response => {
                // check for response errors
                if (response.status !== 201) {
                    error('POST API response failure: ' + response.status);
                    return;
                }
                // valid response
                console.log(data);
                // redirect on successful login
                window.location.href = "{{ site.baseurl }}/note";
                })
                // catch fetch errors (ie Nginx ACCESS to server blocked)
                .catch(err => {
                    error(err + " " + url);
                });
            }
            // Something went wrong with actions or responses
            function error(err) {
                // log as Error in console
                console.log(err);
            }


</script>
<center>

<label for="date" style="color:black;">Date:</label><br>
<input type="text" id="date" name="date" value="MM/DD/YYYY"  maxlength="10" size="4"><br>

<label for="id" style="color:black;" >Club ID:</label><br>
<input type="text" id="id" name="id" value="##"  maxlength="10" size="4"><br><br>

<label for="name" style="color:black;">Name:</label><br>
<input type="text" id="name" name="name" value="aadya daita"  maxlength="10" size="4"><br><br>

<textarea id="text" name="text" rows="4" cols="50">Enter text here</textarea>


<div class="buttons-container">
  <button class="button-arounder" onclick="documents()">Submit (old notes)</button>
</div>
<br>
<h3 id="document_result"></h3>
<br>
<br>


<div class="buttons-container">
  <button class="button-arounder" onclick="signup2()">Submit (new notes)</button>
</div>
<br>
<br>

</center>
