<html>
    <head>
        <style>
            .btn-custom {
                background-color: #198754;
                border-color: #ffffff;
            }
            .btn-custom:hover, .btn-custom:focus, .btn-custom:active, .btn-custom.active, .open>.dropdown-toggle.btn-custom {
                color: #fff;
                background-color: #157347;
                border-color: #ffffff;
            }
        </style>
    </head>
    <body>
        <h1 class="text-center m-5 text-success">Search Results</h1> <!-- Creates main header on page -->
         <div class="mb-3 px-5">
                <input class="form-control" type="text" id="term" name="term" size="50" required placeholder="search clubs"> <!-- input class to search words -- click to search button -->
                <button class="mt-2 btn btn-success" onclick="clubSearch()">Search</button>
                <!--button which activates clubsearch function//class  -->
        </div>  
        <div class="table-responsive mx-5">
            <table class="table table-hover table-bordered border-secondary mb-5">
                <thead>
                    <tr>
                        <th scope="col">ID</th>
                        <th scope="col">Name</th>
                        <th scope="col">Purpose</th>
                        <th scope="col">Club Type(s)</th>
                        <th scope="col">Email</th>
                        <th scope="col">Club President</th>
                        <th scope="col">Staff Advisor</th>
                        <th scope="col">Meeting Time and Location</th>
                        <th scope="col">Additional Info</th>
                        <!-- creates header cells for each topic in the table  -->
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="clubs">
                </tbody>
            </table>
        </div>
        <script>
           // prepare fetch urls
            // const search_url = "http://localhost:8192/api/club/search";
            // origionally was going to use local host but problem with main java because of some update being behind so switched to deployed link 
            const search_url = "https://rebeccaaa.tk/api/club/search";
            const searchContainer = document.getElementById("clubs");
            //declares the scope and what it is looking for 
            function clubSearch(){
            // fetch standard requires database set to a name-value pair
            var term = document.getElementById("term").value;
            //through search we look at terms so this is what the "id" is 
            let data = {term: term};
            console.log(data);
            //prints the parameter regarding data 
            const search_options = {
                method: 'POST',// posting the results to the site because using a new page -- wouldve used get if jsut search bar
                mode: 'cors', //cross origin resourche sharing 
                cache: 'no-cache', //force the browser to check the server to see if the file is different from the file it already has in the cache-- make sure not reusing a url that was never changed 
                credentials: 'include', //deals with cookies, authorization, etc. 
                headers: {
                'Content-Type': 'application/json'
                },
                body: JSON.stringify(data), // convert to JSON
            };
            // fetch the API
            fetch(search_url, search_options)
                // response is a RESTful "promise" on any successful fetch
                .then(response => {
                // check for response errors
                if (response.status !== 200) {
                    error('GET API response failure: ' + response.status);
                    return;
                }
                // valid response will have JSON data
                response.json().then(data => {
                    let i = 1;
                    searchContainer.innerHTML = ""; // origionally had while (resultContainer.firstChild) {resultContainer.removeChild(resultContainer.firstChild);} but chagned to this to clear previous searches 
                    for (const row of data) {
                        console.log(row);
                        // columns
                        const tr = document.createElement("tr");
                        const id = document.createElement("td");
                        const name = document.createElement("td");
                        const purpose = document.createElement("td");
                        const types = document.createElement("td");
                        const email = document.createElement("td");
                        const president = document.createElement("td");
                        const advisor = document.createElement("td");
                        const meeting = document.createElement("td");
                        const info = document.createElement("td");
                        // each creating data table objects for the response to be put into
                        // const official = document.createElement("td");
                        // accessing JSON values
                        id.innerHTML = i;
                        name.innerHTML = row.name;
                        purpose.innerHTML = row.purpose;
                        types.innerHTML = row.types;
                        email.innerHTML = row.email
                        president.innerHTML = row.president;
                        advisor.innerHTML = row.advisor;
                        meeting.innerHTML = row.meeting;
                        info.innerHTML = row.info;
                        // official.innerHTML = row.official;
                        // add all columns to the row
                        //inner elements 
                        tr.appendChild(id);
                        tr.appendChild(name);
                        tr.appendChild(purpose);
                        tr.appendChild(types);
                        tr.appendChild(email);
                        tr.appendChild(president);
                        tr.appendChild(advisor);
                        tr.appendChild(meeting);
                        tr.appendChild(info);
                        // add row to table, and then keep adding for each club that maatches search 
                        searchContainer.appendChild(tr);
                        i++;
                    }    
                })
            })
            // catch fetch errors (ie Nginx ACCESS to server blocked)
            .catch(err => {
                error(err + " " + search_url);
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
                searchContainer.appendChild(tr);
            }
        </script>
    </body>
 <html>
