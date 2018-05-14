# Apuntes sobre PostgreSQL

### Crear, alterar o reiniciar una secuencia en PostgreSQL

```{sql}

# Crear secuencia:
CREATE SEQUENCE foo start 100;

# Borrar secuencia:
DROP SEQUENCE foo; 

# Reiniciar la secuencia a un valor con la función setval:
SELECT setval('foo',1500,'t'); 

# Reiniciarla para que empieze desde el primer valor: 
ALTER SEQUENCE foo restart 1;

```

