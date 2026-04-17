Función SUB — Resta Binaria de 16 bits
SUB — Resta Binaria de 16 bits

Implementa la operación rs - rt en una arquitectura de 16 bits (tipo R), almacenando el resultado en rd:

El circuito opera en tres etapas:

Inversión de B: NOT de 16 bits → ~B
Suma: sumador de 16 bits recibe A y ~B, con Cin = 1 → realiza A + ~B + 1
Overflow: el Cout indica desbordamiento
Ejemplo (4 bits)
5 (0101) - 3 (0011)
→ ~B = 1100
→ ~B + 1 = 1101 (-3)
→ 0101 + 1101 = 0010 (2)

¿Por qué funciona esto? Porque en el sistema de complemento a dos, el número negativo de cualquier valor B se obtiene exactamente haciendo ~B + 1. Entonces restar B es lo mismo que sumar su versión negativa.

Cómo se adapta esto al circuito
El circuito implementa exactamente esa lógica en tres etapas:
1. Inversión de B: Una compuerta NOT de 16 bits recibe el operando B y devuelve ~B, con cada uno de sus 16 bits invertidos simultáneamente.
2. Suma con carry forzado: Un sumador de 16 bits recibe A en una entrada y ~B en la otra. El pin de carry-in (Cin) está conectado a una constante 1, lo que equivale a ese +1 del complemento a dos. El sumador hace entonces A + ~B + 1, que es exactamente A - B.
3. Detección de overflow: El carry-out (Cout) del sumador es una señal de 1 bit que indica si el resultado se fue fuera del rango representable en 16 bits. En operaciones con signo, el overflow ocurre cuando se restan dos números de signos opuestos y el resultado no cabe.
La resta se realiza reutilizando el sumador mediante complemento a dos:

A - B = A + (~B) + 1
~B: inversión de todos los bits de B
+1: convierte a complemento a dos (representación negativa)
Implementación

VENETAJA:
Permite usar el mismo hardware para suma y resta, reduciendo complejidad, área y consumo.
