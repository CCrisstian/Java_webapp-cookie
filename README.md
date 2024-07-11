<h1 align="center">Introducción Cookie en Servlet</h1>
<h2>¿Qué es una Cookie?</h2>
<p>Una cookie son datos del usuario almacenados en el navegador web (lado del cliente) y los servidores la utilizan cuando se comunican con el cliente.</p>
<p align="center"><img width="719" alt="image" src="https://github.com/user-attachments/assets/e0209a22-60e6-4b5d-8d59-99ca05344bcf"></p>
<h2>Manejo de estados</h2>

- Una de las características de las peticiones http es que no manejan estado de los datos del request, por eso es la importancia del manejo de sesiones o cookies http
- Las cookies nos permiten un forma para mantener informacion del usuario entre peticiones y poder recordarlas
- Existen dos formas de mantener información del usuario, una es usando cookies y otra el objeto HttpSession del api servlet.

<h2>Trabajar con Cookies en Servlet</h2>

- Crear una cookie
  - Para enviarla al cliente, necesitamos crearla con un nombre y un valor asociado, luego agregarla a la respuesta:
```java
Cookie username = new Cookie("username", "andres");
response.addCookie(username);
```

- Leer una cookie del request
  - Las cookies son enviadas desde el cliente al servidor
```java
Cookie[] cookies = request.getCookies();
String username = Arrays.stream(cookies)
    .filter(c -> "username".equals(c.getName()))
    .map(Cookie::getValue)
    .findFirst()
    .orElse(null);
```

- Eliminar una cookie
  - Necesitamos crearla nuevamente con mismo nombre y asignando cero en el método setMaxAge:
```java
Cookie username = new Cookie("username", "");
username.setMaxAge(0);
response.addCookie(username);
```

<h2>Métodos importantes</h2>

- setDomain(String dominio)
- getDomain()
```java
Cookie username = new Cookie("username", "andres");
username.setDomain("ejemplo.com");
```
- setMaxAge(int seg)
- getMaxAge()
```java
username.setMaxAge(60*60);
```
- setPath(String path)
- getPath();
```java
cookie.setPath("/webapp");
```
- setValue(String valor)
- getValue()
```java
Cookie username = new Cookie("username", "andres");
username.setValue("admin");
out.println(username.getValue()); // imprime admin
```
- getName()
```java
Cookie username = new Cookie("username", "andres");
out.println(username.getName()); // imprime username
```
