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
            const url = "https://rebeccaaa.tk/search";    
        function clubSearch() {
            location.href ="{{ site.baseurl }}/search";
            // fetch standard requires database set to a name-value pair
            const term = document.getElementById("term");
            const body = {
                term: term.value,
                foo: "bar"
            };
            // fetch call with header options
            fetch('/api/club/search', {
                method: "POST",
                credentials: "include",
                body: JSON.stringify(body),
                cache: "no-cache",
                headers: new Headers({
                    "content-type": "application/json"
                })
            })
            // async then replies with response header
            .then(function (response) {
                // prepare HTML search result container for new output
                const resultContainer = document.getElementById("result");
                // clean up from previous search
                while (resultContainer.firstChild) {
                    resultContainer.removeChild(resultContainer.firstChild);
                }
                // trap error response from Web API
                if (response.status !== 200) {
                    const errorMsg = 'Database response error: ' + response.status;
                    console.log(errorMsg);
                    const div = document.createElement("div");
                    div.innerHTML = errorMsg;
                    resultContainer.appendChild(div);
                    return;
                }
                // response contains valid result
                response.json().then(function(data) {
                    // loop through JSON and build HTML output
                    for (let i = 0; i < data.length; i++) {
                        const div = document.createElement("div");
                        div.innerHTML = data[i].club;
                        resultContainer.appendChild(div);
                    }
                })
            })
        }               
    </script> 
 </head>
 <html>
   
    