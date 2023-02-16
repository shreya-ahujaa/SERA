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
        <script>
            // prepare fetch GET options
            const options = {
                method: 'GET', // *GET, POST, PUT, DELETE, etc.
                // mode: 'cors', // no-cors, *cors, same-origin
                cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
                credentials: 'include', // include, same-origin, omit
                headers: {
                'Content-Type': 'application/json'
                // 'Content-Type': 'application/x-www-form-urlencoded',
                },
            };
            fetch("https://rebeccaaa.tk/hello", options)
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
                })
            });
            // Something went wrong with actions or responses
            function error(err) {
                // log as Error in console
                console.log(err);
            }
        </script>
    </head>
    <body>
        <div class="bg-success w-50 mx-auto m-5">
            <h2 class="text-light mx-5 pt-5">Profile</h2>
            <!-- 'email' is mapped to 'username' for Spring Security -->
            <div class="mb-3 px-5">
                <label class="form-label" for="username">EMAIL</label>
                <p id="email"></p>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="name">CLUB NAME</label>
                <p id="name"></p>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="purpose">PURPOSE</label>
                <p id="purpose"></p>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="types">CLUB TYPE(S)</label>
                <p id="types"></p>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="president">CLUB PRESIDENT</label>
                <p id="president"></p>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="advisor">STAFF ADVISOR</label>
                <p id="advisor"></p>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="meeting">MEETING TIME AND LOCATION</label>
                <p id="meeting"></p>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="info">ADDITIONAL INFO</label>
                <p id="info"></p>
            </div>
            <a class="btn btn-custom text-nowrap text-light my-3 mx-5 mb-4" type="submit" href="{{ site.baseurl }}/update">Update Profile</a>
        </div>  
        <script>
            const storedData = JSON.parse(localStorage.getItem('ID'));
            console.log(storedData);
            // prepare fetch urls
            // const base_url = "http://localhost:8192/api/club/";
            const base_url = "https://rebeccaaa.tk/api/club/";
            const get_by_id = base_url + storedData;
             // fetch the API
            fetch(get_by_id, options)
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
                    document.getElementById("name").innerHTML = data.name;
                    document.getElementById("purpose").innerHTML = data.purpose;
                    document.getElementById("types").innerHTML = data.types;
                    document.getElementById("email").innerHTML = data.email;
                    document.getElementById("president").innerHTML = data.president;
                    document.getElementById("advisor").innerHTML = data.advisor;
                    document.getElementById("meeting").innerHTML = data.meeting;
                    document.getElementById("info").innerHTML = data.info;    
                })
            })
            // catch fetch errors (ie Nginx ACCESS to server blocked)
            .catch(err => {
                error(err + " " + get_by_id);
            });
        </script>  
    </body>    
</html>
