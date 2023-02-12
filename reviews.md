<html>
    <head>
        <style>
            .role {
                color: red;
            }
        </style>
    </head>
    <body>
        <h1 class="text-center m-5 text-success">DNHS CLUB REVIEWS</h1>
        <div class="table-responsive mx-5">
            <table class="table table-hover table-bordered border-secondary mb-5">
                <thead>
                    <tr>
                        <th scope="col">ID</th>
                        <th scope="col">Review</th>
                        <th scope="col">Likes</th>
                        <th scope="col">Dislikes</th>
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="reviews">
                </tbody>
            </table>
        </div>
        <script>
            // prepare fetch urls
            // const review_url = "http://localhost:8192/database/reviews";
            const review_url = "https://rebeccaaa.tk/database/reviews";
            const get_url = review_url + "/25" ;
            const reviewContainer = document.getElementById("reviews");
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
                    for (const row of data) {
                        console.log(row);
                        // columns
                        const tr = document.createElement("tr");
                        const review_id = document.createElement("td");
                        const review = document.createElement("td");
                        const likes = document.createElement("td");
                        const dislikes = document.createElement("td");
                        // accessing JSON values
                        review_id.innerHTML = row.id;
                        review.innerHTML = row.text;
                        likes.innerHTML = row.likes;
                        dislikes.innerHTML = row.dislikes;
                        // add all columns to the row
                        tr.appendChild(review_id);
                        tr.appendChild(review);
                        tr.appendChild(likes);
                        tr.appendChild(dislikes);
                        // add row to table
                        reviewContainer.appendChild(tr);
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
