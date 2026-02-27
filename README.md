## Práctica 4 
Asignatura: Procesadores del Lenguaje
Autor: Marcos Llinares Montes
alu0100972443@ull.edu.es


 ### Preguntas del informe

3.1. Describa la diferencia entre /* skip whitespace */ y devolver un token.

Skip whitespace (\s+): No devuelve ningún token al parser, simplemente consume los espacios en blanco y continúa.
Devolver un token: Devuelve un token que el parser debe procesar. El parser lo recibe y aplica las reglas gramaticales

3.2. Escriba la secuencia exacta de tokens producidos para la entrada 123**45+@.

Para la entrada 123**45+@:

- `123` → `NUMBER` (coincide con `[0-9]+`)
- `**` → `OP` (coincide con "**")
- `45` → `NUMBER` (coincide con `[0-9]+`)
- `+` → `OP` (coincide con `[-+*/`])
- `@` → `INVALID` (coincide con .)
- (fin de entrada) → `EOF`

Secuencia exacta: `NUMBER, OP, NUMBER, OP, INVALID, EOF`


3.3. Indique por qué `**` debe aparecer antes que `[-+*/]`.

En Jison (y en flex), las reglas se evalúan en orden de máxima coincidencia primero, pero cuando hay empate, se aplica la primera regla definida.


3.4. Explique cuándo se devuelve EOF.

`<<EOF>>` es un patrón especial de Jison/Flex que coincide con el final del archivo/entrada.

Se devuelve cuando: Se han consumido todos los caracteres de la entrada. No hay más texto que procesar. Es el último token que recibe el parser.


3.5. Explique por qué existe la regla . que devuelve INVALID.

La regla `.` (punto) en expresiones regulares coincide con cualquier carácter.

Funciona como "cajón de sastre" para el resto de carácteres no considerados y sirve para
1. Captura caracteres no reconocidos: Si ninguna regla anterior coincide, esta lo hace
2. Permite manejo de errores: El parser puede detectar `INVALID` y mostrar un error claro
3. Debe ser la última regla: Como coincide con todo, debe estar al final