<html>
    <body>
        <h1 class="text-center m-5 text-success">DNHS CLUB LIST</h1>
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
            // prepare fetch urls
            // const club_url = "http://localhost:8192/api/club";
            const club_url = "https://rebeccaaa.tk/api/club";
            const get_url = club_url + "/";
            const clubContainer = document.getElementById("clubs");
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
            // fetch the API
            fetch(get_url, options)
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
                        // url containers
                        const minutes = document.createElement("td");
                        const reviews = document.createElement("td");
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
                        var review_str = "{{ site.baseurl }}/reviews?id=" + row.id;
                        reviews.innerHTML = '<a href="' + review_str +'">' + "Reviews for " + row.name + '</a>';
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
                        // tr.appendChild(official);
                        tr.appendChild(minutes);
                        tr.appendChild(reviews);
                        // add row to table
                        clubContainer.appendChild(tr);
                        i++;
                    }    
                })
            })
            // catch fetch errors (ie Nginx ACCESS to server blocked)
            .catch(err => {
                error(err + " " + get_url);
            });
            // Something went wrong with actions or responses
            function error(err) {
                // log as Error in console
                console.error(err);
                // append error to resultContainer
                const tr = document.createElement("tr");
                const td = document.createElement("td");
                td.innerHTML = err;
                tr.appendChild(td);
                clubContainer.appendChild(tr);
            }
        </script>
    </body>
</html>
