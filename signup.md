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
            <h2 class="text-light mx-5 pt-5">SIGN UP</h2>
            <form>
                <table class="table-responsive mx-5">
                    <!-- 'email' is mapped to 'username' for Spring Security -->
                    <tr><th><label for="username">EMAIL</label></th></tr>
                    <tr><td><input type="email" id="username" name="username" size="20" required></td></tr>
                    <tr><th><label for="password">PASSWORD</label></th></tr>
                    <tr><td><input type="password" id="password" name="password" size="20" required></td></tr>
                    <tr><th><label for="name">CLUB NAME</label></th></tr>
                    <tr><td><input type="text" id="name" name="name" size="20" required></td></tr>
                    <tr><th><label for="purpose">PURPOSE</label></th></tr>
                    <tr><td><input type="text" id="purpose" name="purpose" size="100" required></td></tr>
                    <tr><th><label for="types">CLUB TYPE(S)</label></th></tr>
                    <tr><td><input type="text" id="types" name="types" size="20" required></td></tr>
                    <tr><th><label for="president">CLUB PRESIDENT</label></th></tr>
                    <tr><td><input type="text" id="president" name="president" size="20" required></td></tr>
                    <tr><th><label for="advisor">STAFF ADVISOR</label></th></tr>
                    <tr><td><input type="text" id="advisor" name="advisor" size="20" required></td></tr>
                    <tr><th><label for="meeting">MEETING TIME AND LOCATION</label></th></tr>
                    <tr><td><input type="text" id="meeting" name="meeting" size="20" required></td></tr>
                    <tr><th><label for="info">ADDITIONAL INFO</label></th></tr>
                    <tr><td><input type="text" id="info" name="info" size="20" required></td></tr>
                </table>
                <button class="btn btn-custom text-nowrap text-light my-3 mx-5" type="submit">Sign Up</button>
            </form>
            <div class="text-light mx-5 pb-3">
                <p class="login">Already registered your club? <a class="text-light" href="{{ site.baseurl }}/login">Log In</a></p>
            </div>
        </div>
    </body>
</html>