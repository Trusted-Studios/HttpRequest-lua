# HttpRequest in LUA / FiveM environment

## How it works
> ...

### Lua Code
```lua
function GetCodeToExecute(key)
    PerformHttpRequest("https://trusted-service.com/assets/scriptname?key="..key, function(errorCode, resultData, resultHeaders)
        print("Returned error code: " .. tostring(errorCode))
        print("Returned data: " .. tostring(resultData))
        print("Returned result headers: " .. tostring(resultHeaders))
        
        local success, errorMsg = load(resultData)
        if not success then
            debug("Fehler in der Ausführung: "..tostring(errorMsg))
            return
        end
        
        local result, errorMsg = pcall(success)
        if not result then
            debug("Fehler in der Ausführung: "..tostring(errorMsg))
            return
        end
        
        debug("Webcode wurde ausgeführt")
    end)
end
```

### Website #php
> Simple `php` code as a webkey api
```php
<?php
if ($_GET["key"] != "123456") {
    die("Ungültiger Schlüssel");
}

if ($_GET["type"] == "ts_system") {
    $host = "localhost";
    $user = "meinBenutzername";
    $pass = "meinPasswort";
    $db = "meineDatenbank";
    $conn = new mysqli($host, $user, $pass, $db);

    if ($conn->connect_error) {
        die("Verbindung zur Datenbank fehlgeschlagen: " . $conn->connect_error);
    }

    
    $sql = "SELECT * FROM meineTabelle";
    $result = $conn->query($sql);

    if (!$result) {
        die("Abfrage fehlgeschlagen: " . $conn->error);
    }

    
    $data = array();
    while ($row = $result->fetch_assoc()) {
        $data[] = $row;
    }

    $conn->close();

    header('Content-Type: application/json');
    echo json_encode($data);
} else {
    die("Ungültiger Abfragetyp");
}
```
