Suppose, after clicking a button we want to post a list of Id from a table to **example_one** view in our **views.py** file in the **examplefolder** folder. So in our .html file :

    <script>
        var url = "{% url 'examplefolder:example_one' %}";
        var i = 0;     
        var clicked = false;

        function getCookie(name) {
            var cookieValue = null;
            if (document.cookie && document.cookie != '') {
                var cookies = document.cookie.split(';');
                for (var i = 0; i < cookies.length; i++) {
                    var cookie = jQuery.trim(cookies[i]);
                    // Does this cookie string begin with the name we want?
                    if (cookie.substring(0, name.length + 1) == (name + '=')) {
                        cookieValue = decodeURIComponent(cookie.substring(name.length + 1));
                        break;
                    }
                }
            }
            return cookieValue;
        }
        var csrftoken = getCookie('csrftoken');

        function csrfSafeMethod(method) {

            return (/^(GET|HEAD|OPTIONS|TRACE)$/.test(method));
        }

        function sameOrigin(url) {
            //test that a given url is a same-origin URL
            //url could be relative or scheme relative or absolute
            var host = document.local.host;
            var protocol = document.location.protocol;
            var sr_origin = '//' + host;
            var origin = protocol + sr_origin;

            return (url == origin || url.slice(0, origin.length + 1) == origin + '/') ||
                (url == sr_origin || url.slice(0, sr_origin.length + 1) == sr_origin + '/') ||
                !(/^(\/\/|http:|https:).*/.test(url));
        }

        $.ajaxSetup({
            beforeSend: function (xhr, settings) {
                /*if (!csrfSafeMethod(settings.type) && sameOrigin(settings.url)) {
                 // Send the token to same-origin, relative URLs only.
                 // Send the token only if the method warrants CSRF protection
                 // Using the CSRFToken value acquired earlier
                 xhr.setRequestHeader("X-CSRFToken", csrftoken);
                 }*/
                xhr.setRequestHeader("X-CSRFToken", csrftoken);
            }
        });
        function addcheckedid(csrftoken, exampleid,totalamount) {
      
                $.post(url,
                    {'csrftoken': csrftoken, 'id[]': exampleid, 'totalamount':totalamount},
                    function (data, status) {

                        alert(data);


                    });
                
        }




        $(document).ready(function () {

             $("#btn").click(function () {
                
                var type = $("#btn").attr("type");
                var table = document.getElementById("table-example");
                if (type == "button") {
                    
                    if (table.rows.length > 1) {

                        var j = 0;
                        exampleid = [];
                        //iterate through rows
                        for (var k = 1, row; row = table.rows[k]; k++) {
                            
                            if (row.cells[0].innerHTML != "") {
                                
                                //iterate through columns
                                    exampleid[j] = row.cells[0].innerHTML;
                                    j++;


                            }

                        }
                        
                        totalamount = document.getElementById("sum").innerHTML;
                       
                        if (exampleid.length > 0) {
                            addcheckedid(csrftoken, exampleid,totalamount);
                        } else {
                            alert("No data to post!!");
                        }
                    }
                }
            });

        })
    </script>
