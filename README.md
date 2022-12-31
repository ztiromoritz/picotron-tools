# picotron-tools

Paste this to playground terminal.

```
save_object("system/less.lua", [[

    local path = env().argv[1] or ""
    function _init()
        current_line = 0
        s = load_object(path)
        lines = {}
        for t in string.gmatch(s, "[^\n]+") do
            add(lines, t)
        end
    end

    function _update()
        if get_key_pressed("up") then
            current_line = current_line - 1
        end
        if get_key_pressed("down") then
            current_line = current_line + 1
        end
        if get_key_pressed("q") then
            exit()
        end
    end
    function _draw()
        cls()
        for i = 0, 21 do
            print(i + 1 + current_line, 0, (i + 1) * 12, 4)
            print(lines[i + current_line], 30, (i + 1) * 12, 3)
    end
    rectfill(0, 0, 480, 8, 9)
    print("\125 Use ArrowUp/Down '" .. path .. "'" .. #lines, 0, 0, 2)
end
]])
```

Use it like this

```
less system/api.lua
```

Use ArrowUp/Down for scroll to text and q for quit.
