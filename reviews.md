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
        <div>
        <h2 class="text-left m-5 text-success">Add Review</h2>
        <input type="text" id="review" name="review" size="20" required>
        <button class="btn btn-success text-nowrap my-3 mx-5" type="submit" onclick="add_review()">Add</button>
        </div>
        <script type="text/javascript">
            // prepare fetch urls
            // const review_url = "http://localhost:8192/database/reviews";
            const review_url = "https://rebeccaaa.tk/database/reviews";
            const params = new URLSearchParams(window.location.search);
            let club_id = params.get("id");
            const get_url = review_url + "/" + club_id;
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
                        likes.innerHTML = '<a href="#" onclick="like_review(\'' + row.id + '\')">' + row.likes + '</a>';
                        dislikes.innerHTML = '<a href="#" onclick="dislike_review(\'' + row.id + '\')">' + row.dislikes + '</a>';
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
                console.log(err);
                // append error to resultContainer
                const tr = document.createElement("tr");
                const td = document.createElement("td");
                td.innerHTML = err;
                tr.appendChild(td);
                reviewContainer.appendChild(tr);
            }
            const addreview_url = "https://rebeccaaa.tk/database/addreview/" + club_id;
            function add_review(){
                var review_text = document.getElementById("review").value;
                // store data in JavaScript object
                console.log(review_text);
                const options = {
                    method: 'POST',
                    mode: 'cors',
                    cache: 'no-cache',
                    credentials: 'include',
                    headers: {
                    'Content-Type': 'text/html; charset=utf-8'
                    },
                    body: review_text, // convert to JSON
                };
                fetch(addreview_url, options)
                .then(response => {
                    // check for response errors
                    if (response.status !== 201) {
                        error('POST API response failure: ' + response.status);
                        return;
                    }
                    // valid response
                    console.log(review_text);
                    // redirect on successful add review
                    window.location.href = window.location;
                }) 
                // catch fetch errors (ie Nginx ACCESS to server blocked)
                .catch(err => {
                    error(err + " " + url);
                });
            }    
            function like_review(review_id){
                // store data in JavaScript object
                const options = {
                    method: 'POST',
                    mode: 'cors',
                    cache: 'no-cache',
                    credentials: 'include',
                    headers: {
                    'Content-Type': 'text/html; charset=utf-8'
                    },
                };
                var like_api_url = "https://rebeccaaa.tk/database/like/" + review_id;
                fetch(like_api_url, options)
                .then(response => {
                    // check for response errors
                    if (response.status !== 200) {
                        error('POST API response failure: ' + response.status);
                        return;
                    }
                    // redirect on successful add review
                    window.location.href = window.location;
                }) 
                // catch fetch errors (ie Nginx ACCESS to server blocked)
                .catch(err => {
                    error(err + " " + like_api_url);
                });
            } 
            function dislike_review(review_id){
                // store data in JavaScript object
                const options = {
                    method: 'POST',
                    mode: 'cors',
                    cache: 'no-cache',
                    credentials: 'include',
                    headers: {
                    'Content-Type': 'text/html; charset=utf-8'
                    },
                };
                var dislike_api_url = "https://rebeccaaa.tk/database/dislike/" + review_id;
                fetch(dislike_api_url, options)
                .then(response => {
                    // check for response errors
                    if (response.status !== 200) {
                        error('POST API response failure: ' + response.status);
                        return;
                    }
                    // redirect on successful add review
                    window.location.href = window.location;
                }) 
                // catch fetch errors (ie Nginx ACCESS to server blocked)
                .catch(err => {
                    error(err + " " + dislike_api_url);
                });
            }    
        </script>
    </body>
</html>
