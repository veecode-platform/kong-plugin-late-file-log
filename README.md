# kong-plugin-late-file-log

A derived file-log plugin with a very late ordering (for OSS).

Needed because there is no way to control the order of plugins in the community edition of Kong.

# Install:

curl -X POST --header "$KONG_AUTH" http://localhost:8001/services/{id}/plugins \
  --data "name=late-file-log" \
  --data "config.path=/dev/stdout"

# Notes

The `schema.lua` and `handler.lua` files are copies from the original `file-log` plugin:

```sh
wget https://raw.githubusercontent.com/Kong/kong/master/kong/plugins/file-log/schema.lua -q -O ./late-file-log/schema.lua
sed -i '' 's/  name =.*/  name = "late-file-log",/g' ./late-file-log/schema.lua
wget https://raw.githubusercontent.com/Kong/kong/master/kong/plugins/file-log/handler.lua -q -O ./late-file-log/handler.lua
sed -i '' 's/FileLogHandler/LateFileLogHandler/g' ./late-file-log/handler.lua
sed -i '' 's/  PRIORITY =.*/  PRIORITY = 1800,/g' ./late-file-log/handler.lua
```

