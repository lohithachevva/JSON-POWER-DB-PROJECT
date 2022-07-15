# getall.html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
    <script src="https://login2explore.com/jpdb/resources/js/0.0.3/jpdb-commons.js"></script>
    <title>Get All Using PowerDB</title>
</head>

<body>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
            <a class="navbar-brand" href="/home.html">JSONPowerDB CRUD Project</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <li class="nav-item">
                        <a class="nav-link active" aria-current="page" href="/home.html">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link"
                            href="https://login2explore.com/jpdb/docs.html#jpdb-command-request">Reference</a>
                    </li>
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button"
                            data-bs-toggle="dropdown" aria-expanded="false">
                            DB Access
                        </a>
                        <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                            <li><a class="dropdown-item" target="_blank" href="/getAll.html">GET ALL IN DB</a></li>
                            <li><a class="dropdown-item" target="_blank" href="/getByKey.html">GET BY KEY</a></li>
                            <!-- <li><hr class="dropdown-divider"></li> -->
                            <li><a class="dropdown-item" target="_blank" href="/getByRecord.html">GET BY RECORD</a></li>
                            <li><a class="dropdown-item" target="_blank" href="/put.html">PUT METHOD</a></li>
                            <li><a class="dropdown-item" target="_blank" href="/update.html">UPDATE IN DB</a></li>
                            <li><a class="dropdown-item" target="_blank" href="/delete.html">REMOVE IN DB</a></li>
                        </ul>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link disabled">
                            <-- CRUD Oprations Using JSONPowerDB</a>
                    </li>
                </ul>
                <!-- <form class="d-flex">
              <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
              <button class="btn btn-outline-success" type="submit">Search</button>
            </form> -->
            </div>
        </div>
    </nav>

    <div class="container">

        <h1 class="my-5">Get All Records Of A DB Using PowerDB</h1>

        NOTE:
        <ul>
            <li>First you need to have a idea of how many databases and relations are present in the database.</li>
            <li>For that, below there are tow boxes called "find all databases" & "find all relations", where you can find out how many databases and relations are present.</li>
            <li>To find out databases, simply click on the "get all db" button and you'll get a bunch of databases. </li>
            <li>If you'll not see the databases coming then you need to create databases and relations in the "put method" in the "<a href="/put.html" target="_blank">PUT page</a>".</li>
            <li>Once you find the database and relation, you can put them in the top of the page database and relation section and get all the data containing in the DB.</li>
        </ul>

        <form>
            <div class="mb-3">
                <label for="database" class="form-label">Dadabase</label>
                <input type="text" class="form-control" id="database" aria-describedby="emailHelp"
                    placeholder="Your database name">
            </div>
            <div class="mb-3">
                <label for="relation" class="form-label">Relation</label>
                <input type="text" class="form-control" id="relation" placeholder="Your relation name">
            </div>
            <!-- <button type="submit" class="btn btn-primary">Submit</button> -->
            <input type="button" class="btn btn-primary" id="empSave" value="Submit" onclick="getAllRecords();" />
        </form>

        <br>
        <h2>All records of your DB</h2>
        <textarea name="txtArea" id="txtAreaGetAll" cols="100" rows="10" readonly></textarea>

        <hr>
        <h4 class="my-4">Find All Databases</h4>
        <input type="button" class="btn btn-primary" id="getDb" value="GET All DB" onclick="getAllDb()" />
        <br>
        <textarea class="my-3" style="resize: none;" name="txtArea" id="txtAreaDB" cols="100" rows="10"
            readonly></textarea>
        <br>
        <h4 class="my-4">Find All Relations</h4>
        <div class="mb-3">
            <input type="text" class="form-control" id="getallrelation" placeholder="Database Name">
            <input type="button" class="btn btn-primary my-2" id="getallrel" value="GET All RELATIONS"
                onclick="getAllRelation();" />
            <br>
            <textarea style="resize: none;" name="txtArea" id="txtAreaRel" cols="100" rows="10" readonly></textarea>

        </div>


        <script>

            function getAllDb() {
                let getalldb = getAllDB();
                console.log(getalldb)
                jQuery.ajaxSetup({ async: false });
                var resultObj = executeCommandAtGivenBaseUrl(getalldb, "http://api.login2explore.com:5577", "/api/irl");
                document.getElementById("txtAreaDB").innerText = JSON.stringify(resultObj);
                jQuery.ajaxSetup({ async: true });
            }

            function getAllDB() {
                var getall = `
                {
                    "token": "90939257|-31949286895072591|90939680",
                    "cmd": "GET_ALL_DB"
                }`;
                return getall;
            }

            function getAllRelation() {
                let db = $("#getallrelation").val();
                let getalldb = getrelationjsonstr(db);
                console.log(getalldb)
                jQuery.ajaxSetup({ async: false });
                var resultObj = executeCommandAtGivenBaseUrl(getalldb, "http://api.login2explore.com:5577", "/api/irl");
                document.getElementById("txtAreaRel").innerText = JSON.stringify(resultObj);
                jQuery.ajaxSetup({ async: true });
            }

            function getrelationjsonstr(db) {
                var getall = `
                {
                    "token": "90939257|-31949286895072591|90939680",
                    "cmd": "GET_ALL_RELATIONS",
                    "dbName": "${db}"
                }`;
                return getall;
            }

            function getAllRecords() {
                let db = $("#database").val();
                let rel = $("#relation").val();

                let getall = getallrecords(db, rel);

                console.log(getall);

                jQuery.ajaxSetup({ async: false });
                var resultObj = executeCommandAtGivenBaseUrl(getall, "http://api.login2explore.com:5577", "/api/irl");
                document.getElementById("txtAreaGetAll").innerText = JSON.stringify(resultObj);
                jQuery.ajaxSetup({ async: true });

                $("#database").val("");
                $("#relation").val("");
            }

            function getallrecords(db, rel) {
                let allrecords = `
                {
                    
    "token": "90939257|-31949286895072591|90939680",
    "dbName": "${db}",
    "cmd": "GET_ALL",
    "rel": "${rel}",
    "pageNo": 1,
    "pageSize": 100,
    "createTime": true,
    "updateTime": true
                }
                `;
                return allrecords;
            }

        </script>


        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"
            integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p"
            crossorigin="anonymous"></script>

</body>

</html>
