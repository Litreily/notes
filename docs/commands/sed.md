# sed

## 替换匹配项

```zsh
# not change source file
sed -n 's/pattern/updated/p' file

# change source file, shoule be careful
sed -i 's/pattern/updated/' file
```

## 替换首个匹配项

```zsh
sed -i "0,/pattern/ s/pattern/updated/" file
```

