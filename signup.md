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
            const signup_url = "https://rebeccaaa.tk/api/club/post";
            // const signup_url = "http://localhost:8192/api/club/post";
            function signup(){
                var email = document.getElementById("username").value;
                var password = document.getElementById("password").value;
                var name = document.getElementById("name").value;
                var purpose = document.getElementById("purpose").value;
                var types = document.getElementById("types").value;
                var president = document.getElementById("president").value;
                var advisor = document.getElementById("advisor").value;
                var meeting = document.getElementById("meeting").value;
                var info = document.getElementById("info").value;
                // store data in JavaScript object
                let data = {email: email, password: password, name: name, types: types, purpose: purpose, president: president, advisor: advisor, meeting: meeting, info: info, official: null};
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
                window.location.href = "{{ site.baseurl }}/";
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
            <h2 class="text-light mx-5 pt-5">SIGN UP</h2>
            <!-- 'email' is mapped to 'username' for Spring Security -->
            <div class="mb-3 px-5">
                <label class="form-label" for="username">EMAIL</label>
                <input class="form-control" type="email" id="username" name="username" size="20" required>
            </div>
            <div class="mb-3 px-5">    
                <label class="form-label" for="password">PASSWORD</label>
                <input class="form-control" type="password" id="password" name="password" size="20" required>
            </div>    
            <div class="mb-3 px-5">
                <label class="form-label" for="name">CLUB NAME</label>
                <input class="form-control" type="text" id="name" name="name" size="20" required>
            </div>    
            <div class="mb-3 px-5">               
                <label class="form-label" for="purpose">PURPOSE</label>
                <input class="form-control" type="text" id="purpose" name="purpose" size="100" required>
            </div>    
            <div class="mb-3 px-5">        
                <label class="form-label" for="types">CLUB TYPE(S)</label>
                <input class="form-control" type="text" id="types" name="types" size="20" required placedholder="Advocacy/Awareness, Cultural, Environment, Service, STEM, Visual/Performing Arts">
            </div>    
            <div class="mb-3 px-5">        
                <label class="form-label" for="president">CLUB PRESIDENT</label>
                <input class="form-control" type="text" id="president" name="president" size="20" required>
            </div>    
            <div class="mb-3 px-5">        
                <label class="form-label" for="advisor">STAFF ADVISOR</label>
                <input class="form-control" type="text" id="advisor" name="advisor" size="20" required>
            </div>    
            <div class="mb-3 px-5">        
                <label class="form-label" for="meeting">MEETING TIME AND LOCATION</label>
                <input class="form-control" type="text" id="meeting" name="meeting" size="20" required>
            </div>
            <div class="mb-3 px-5">        
                <label class="form-label" for="info">ADDITIONAL INFO</label>
                <input class="form-control" type="text" id="info" name="info" size="20">
            </div>
            <button class="btn btn-custom text-nowrap text-light my-3 mx-5" type="submit" onclick="signup()">Sign Up</button>
            <div class="text-light mx-5 pb-3">
                <p class="login">Already registered your club? <a class="text-light" href="{{ site.baseurl }}/login">Log In</a></p>
            </div>
        </div>
    </body>
</html>
