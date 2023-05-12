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
```lua
<html>
  <p>Hello World</p>
</html>
```
