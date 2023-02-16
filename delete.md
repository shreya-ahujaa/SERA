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
            const delete_url = "https://rebeccaaa.tk/api/club/delete/";
            // const delete_url = "http://localhost:8192/api/club/delete/";
            const storedData = JSON.parse(localStorage.getItem('ID'));
            console.log(storedData);
            const delete_url_with_id = delete_url + storedData;
            function delete_club(){
                console.log(delete_url);
                const options = {
                    method: 'POST',
                    mode: 'cors',
                    cache: 'no-cache',
                    credentials: 'include',
                     headers: {
                        'Content-Type': 'application/json'
                    },
                };
                fetch(delete_url_with_id, options)
                .then(response => {
                // check for response errors
                if (response.status !== 200) {
                    error('POST API response failure: ' + response.status);
                    return;
                }
                // valid response
                console.log(delete_url);
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
        <h2 class="text-light mx-5 pt-5">Delete Club</h2>
        <div class="mb-3 px-5">
            <p>Warning: Clicking the button below will delete your club. It is a destructive action that cannot be undone.</p>
        </div>
        <button class="btn btn-custom text-nowrap text-light my-3 mx-5 mb-4" type="submit" onclick="delete_club()">Delete</button>
     </div>       
 </body>
</html>
