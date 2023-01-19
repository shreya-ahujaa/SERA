<html>
    <head>
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
                <button class="btn btn-outline-light text-nowrap text-light mt-3 m-5" type="submit">Log In</button>
            </form>
        </div>
    </body>
</html>