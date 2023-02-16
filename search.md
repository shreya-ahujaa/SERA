<html>
    <head>
        <style>
            .btn-custom {
                color: #fff;
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
        <h1 class="text-center m-5 text-success">Search Results</h1>
         <form class="d-flex" role="search">
                <input type="text" class="form-control" id="term" placeholder="Search Club">
        </form>
        <label></label>
        <button class="btn btn-success" onclick="clubSearch()">Search</button>
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
                        <!-- <th scope="col">Official Club?</th> -->
                        <!-- Links -->
                        <th scope="col">Meeting Minutes</th>
                        <th scope="col">Reviews</th>
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="clubs">
                </tbody>
            </table>
        </div>
        <script>
            // fetch standard requires database set to a name-value pair
            const term = document.getElementById("term");
            const data = {
                term: term.value,
            };
           // prepare fetch urls
            const search_url = "https://rebeccaaa.tk/api/club/search";
            // const search_url = "https://rebeccaaa.tk/api/club/search";
            const searchContainer = document.getElementById("clubs");
            const search_options = {
                method: 'POST',
                mode: 'cors',
                cache: 'no-cache',
                credentials: 'include',
                headers: {
                'Content-Type': 'application/json'
                },
                body: JSON.stringify(data), // convert to JSON
            };
            function clubSearch(){
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
                        tr.appendChild(id);
                        tr.appendChild(name);
                        tr.appendChild(purpose);
                        tr.appendChild(types);
                        tr.appendChild(email);
                        tr.appendChild(president);
                        tr.appendChild(advisor);
                        tr.appendChild(meeting);
                        tr.appendChild(info);
                        // add row to table
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
