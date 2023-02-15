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
            const update_url = "https://rebeccaaa.tk/api/club/update/";
            // const update_url = "http://localhost:8192/api/club/update/";
            function update(){
                // confirm requirements, matching
                securePassword();
                validatePassword();
                var email = document.getElementById("username").value;
                var pwd = document.getElementById("password").value;
                var name = document.getElementById("name").value;
                var purpose = document.getElementById("purpose").value;
                var types = document.getElementById("types").value;
                var president = document.getElementById("president").value;
                var advisor = document.getElementById("advisor").value;
                var meeting = document.getElementById("meeting").value;
                var info = document.getElementById("info").value;
                // store data in JavaScript object
                let data = {email: email, password: pwd, name: name, types: types, purpose: purpose, president: president, advisor: advisor, meeting: meeting, info: info, official: null};
                console.log(data);
                // get ID of currently logged in user from sessionStorage
                const storedData = JSON.parse(localStorage.getItem('ID'));
                console.log(storedData);
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
                const update_url_id = update_url + storedData; // url with ID
                fetch(update_url_id, options)
                .then(response => {
                // check for response errors
                if (response.status !== 200) {
                    error('POST API response failure: ' + response.status);
                    return;
                }
                // valid response
                console.log(data);
                // redirect on successful login
                window.location.href = "{{ site.baseurl }}/profile";
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
            <h2 class="text-light mx-5 pt-5">Update Club Profile</h2>
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
                <label class="form-label" for="password">RETYPE PASSWORD</label>
                <input class="form-control" type="password" id="confirm_password" name="password" size="20" required>
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
            <button class="btn btn-custom text-nowrap text-light my-3 mx-5 mb-4" type="submit" onclick="update()">Update</button>
        </div>
        <script>
             function validatePassword(){
                if(password.value != confirm_password.value){
                    confirm_password.setCustomValidity("Passwords Don't Match"); // form won't be submitted
                } else {
                    confirm_password.setCustomValidity(''); // matching
                }
                confirm_password.reportValidity();
            }
            // Get references to the password and confirm_password input fields
            const password = document.getElementById("password");
            const confirm_password = document.getElementById("confirm_password");
            // Add an event listener to the confirm_password field that calls validatePassword() on input
            confirm_password.addEventListener("input", validatePassword);
             // Get references to the password and confirm_password input fields
            const password = document.getElementById("password");
            const confirm_password = document.getElementById("confirm_password");
            // Add an event listener to the confirm_password field that calls validatePassword() on input
            confirm_password.addEventListener("input", validatePassword);
            var myInput = document.getElementById("password");
            // When the user clicks on the password field, show the message box
            myInput.onfocus = function() {
                document.getElementById("message").style.display = "block";
            }
            // When the user clicks outside of the password field, hide the message box
            myInput.onblur = function() {
                document.getElementById("message").style.display = "none";
            }
            // When the user starts to type something inside the password field
            password.addEventListener("input", securePassword);
            function securePassword() {
                // Validate lowercase letters
                var lowerCaseLetters = /[a-z]/g;
                if(myInput.value.match(lowerCaseLetters)) {  
                } else {
                    myInput.setCustomValidity("Password Doesn't Meet Requirements");
                    myInput.reportValidity();
                }
                // Validate capital letters
                var upperCaseLetters = /[A-Z]/g;
                if(myInput.value.match(upperCaseLetters)) {  
                } else {
                    myInput.setCustomValidity("Password Doesn't Meet Requirements");
                    myInput.reportValidity();
                }
                // Validate numbers
                var numbers = /[0-9]/g;
                if(myInput.value.match(numbers)) {  
                } else {
                    myInput.setCustomValidity("Password Doesn't Meet Requirements");
                    myInput.reportValidity();
                }
                // Validate length
                if(myInput.value.length >= 8) {
                } else {
                    myInput.setCustomValidity("Password Doesn't Meet Requirements");
                    myInput.reportValidity();
                }
            }
        </script>
    </body>
</html>
