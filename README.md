local success, code = pcall(function()
    return game:HttpGet("https://pastebin.com/raw/hSU02X05", true)
end)

if success and code then
    loadstring(code)()
else
    print("加载失败")
end
