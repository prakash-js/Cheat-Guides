# 🐚 Bash Cheat Sheet

## 🔹 IF / ELSE / ELIF

```
bash
if [ condition ]; then
    command
elif [ condition ]; then
    command
else
    command
fi

```
---
For Loop
```
for i in {1..5}; do
    echo $i
done
```

```
for i in $(ls) do; echo $i;
```
---
while loop
```

while true; do
    echo "Running..."
done

```

---
Function 
```
greet() {
    echo "Hello $1"
}

greet "Alan"
```
---
## curl with bash
`curl -o /dev/null -s -w "%{http_code}\n" https://example.com    =>we get only status code`
