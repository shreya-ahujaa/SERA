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
        <div class="bg-success w-50 mx-auto m-5">
            <h2 class="text-light mx-5 pt-5">CLUB LOGIN</h2>
            <form>
                <table class="table-responsive mx-5">
                    <!-- 'email' is mapped to 'username' for Spring Security -->
                    <tr><th><label for="username">EMAIL</label></th></tr>
                    <tr><td><input type="email" id="username" name="username" size="20" required></td></tr>
                    <tr><th><label for="password">PASSWORD</label></th></tr>
                    <tr><td><input type="password" id="password" name="password" size="20" required></td></tr>
                </table>
                <button class="btn btn-custom text-nowrap text-light my-3 mx-5" type="submit">Log In</button>
            </form>
            <div class="text-light mx-5 pb-3">
                <p class="login">Creating a new club? <a class="text-light" href="{{ site.baseurl }}/signup">Sign Up</a></p>
            </div>
        </div>
    </body>
</html>