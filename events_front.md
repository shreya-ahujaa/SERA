# Events Frontend
<!-- HTML table fragment for page -->
<table>
  <thead>
  <tr>
    <th>Event</th>
    <th>Will Attent</th>
    <th>Will Skip</th>
  </tr>
  </thead>
  <tbody id="result">
    <!-- javascript generated data -->
  </tbody>
</table>

<!-- Script is layed out in a sequence (without a function) and will execute when page is loaded -->
<script>

  // prepare HTML defined "result" container for new output
  const resultContainer = document.getElementById("result");

  // keys for event reactions
  const ATTEND = "attend";
  const SKIP = "skip";

  const url = "https://rebeccaaa.tk/api/event/";
  //const get_url = url +"/";
  const attend_url = url + "/attend/";  // attend reaction
  const skip_url = url + "/skip/";  // skip reaction

  // prepare fetch GET options
  const options = {
    method: 'GET', // *GET, POST, PUT, DELETE, etc.
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'same-origin', // include, same-origin, omit
    headers: {
      'Content-Type': 'application/json'
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
  };
  // prepare fetch PUT options, clones with JS Spread Operator (...)
  const put_options = {...options, method: 'PUT'}; // clones and replaces method

  // fetch the API
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
          for (const row of data) {
            // make "tr element" for each "row of data"
            const tr = document.createElement("tr");
            
            // td for event cell
            const event = document.createElement("td");
              event.innerHTML = row.id + ". " + row.event;  // add fetched data to innerHTML

            // td for attend cell with onclick actions
            const attend = document.createElement("td");
              const attend_but = document.createElement('button');
              attend_but.id = ATTEND+row.id   // establishes a attend JS id for cell
              attend_but.innerHTML = row.attend;  // add fetched "attend count" to innerHTML
              attend_but.onclick = function () {
                // onclick function call with "like parameters"
                reaction(ATTEND, attend_url+row.id, attend_but.id);  
              };
              attend.appendChild(attend_but);  // add "attend button" to attend cell

            // td for skip cell with onclick actions
            const skip = document.createElement("td");
              const skip_but = document.createElement('button');
              skip_but.id = SKIP+row.id  // establishes a skip JS id for cell
              skip_but.innerHTML = row.skip;  // add fetched "skip count" to innerHTML
              skip_but.onclick = function () {
                // onclick function call with "jeer parameters"
                reaction(SKIP, skip_url+row.id, skip_but.id);  
              };
              skip.appendChild(skip_but);  // add "skip button" to skip cell
             
            // this builds ALL td's (cells) into tr (row) element
            tr.appendChild(event);
            tr.appendChild(attend);
            tr.appendChild(skip);

            // this adds all the tr (row) work above to the HTML "result" container
            resultContainer.appendChild(tr);
          }
      })
  })
  // catch fetch errors (ie Nginx ACCESS to server blocked)
  .catch(err => {
    error(err + " " + get_url);
  });

  // Reaction function to likes or jeers user actions
  function reaction(type, put_url, elemID) {

    // fetch the API
    fetch(put_url, put_options)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors
      if (response.status !== 200) {
          error("PUT API response failure: " + response.status)
          return;  // api failure
      }
      // valid response will have JSON data
      response.json().then(data => {
          console.log(data);
          // Likes or Jeers updated/incremented
          if (type === ATTEND) // like data element
            document.getElementById(elemID).innerHTML = data.attend;  // fetched attend data assigned to attend Document Object Model (DOM)
          else if (type === SKIP) // jeer data element
            document.getElementById(elemID).innerHTML = data.skip;  // fetched skip data assigned to skip Document Object Model (DOM)
          else
            error("unknown type: " + type);  // should never occur
      })
    })
    // catch fetch errors (ie Nginx ACCESS to server blocked)
    .catch(err => {
      error(err + " " + put_url);
    });
    
  }

  // Something went wrong with actions or responses
  function error(err) {
    // log as Error in console
    console.error(err);
    // append error to resultContainer
    const tr = document.createElement("tr");
    const td = document.createElement("td");
    td.innerHTML = err;
    tr.appendChild(td);
    resultContainer.appendChild(tr);
  }

</script>