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
        <script type="text/javascript">
            const url = "https://rebeccaaa.tk/authenticate";
            // const url = "http://localhost:8192/authenticate";
            function login(){
                var email = document.getElementById("username").value;
                var password = document.getElementById("password").value;
                // store data in JavaScript object
                let data = {email: email, password: password};
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
                fetch(url, options)
                .then(response => {
                // check for response errors
                if (response.status !== 200) {
                    error('POST API response failure: ' + response.status);
                    return;
                }
                // valid response
                console.log(data);
                // redirect on successful login
                window.location.href = "{{ site.baseurl }}/SERA/";
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
    </head>
    <body>
        <div class="bg-success w-50 mx-auto m-5">
            <h2 class="text-light mx-5 pt-5">CLUB LOGIN</h2>
            <!-- 'email' is mapped to 'username' for Spring Security -->
            <div class="mb-3 px-5">
                <label class="form-label" for="username">EMAIL</label>
                <input class="form-control" type="email" id="username" name="username" size="20" required>
            </div>    
            <div class="mb-3 px-5">
                <label class="form-label" for="password">PASSWORD</label>
                <input class="form-control" type="password" id="password" name="password" size="20" required>
            </div>    
            <button class="btn btn-custom text-nowrap text-light my-3 mx-5" type="submit" onclick="login()">Log In</button>
            <div class="text-light mx-5 pb-3">
                <p class="login">Creating a new club? <a class="text-light" href="{{ site.baseurl }}/signup">Sign Up</a></p>
            </div>
        </div>
    </body>
</html>
