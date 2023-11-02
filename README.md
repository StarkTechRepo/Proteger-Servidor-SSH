# Proteger Servidor SSH

---

## ¿Que es y Para que se Usa SSH?:
- SSH, o Secure Shell, es un protocolo de red seguro que permite a los usuarios conectarse a un servidor de forma remota de forma segura. Se utiliza para una variedad de propósitos, incluyendo:

#### Administración de sistemas
- SSH se utiliza comúnmente para administrar sistemas remotos. Los administradores de sistemas pueden utilizar SSH para conectarse a un servidor y realizar tareas como instalar software, configurar servicios y solucionar problemas.

#### Transferencia de archivos
- SSH también se puede utilizar para transferir archivos entre sistemas. El comando scp se utiliza para copiar archivos de forma segura entre sistemas locales y remotos.

#### Acceso remoto
- SSH se puede utilizar para acceder a un sistema remoto de forma remota. Esto puede ser útil para acceder a un sistema que no está físicamente accesible.

#### Encriptación
- SSH utiliza cifrado para proteger las comunicaciones entre el cliente y el servidor. Esto ayuda a proteger las contraseñas y otros datos confidenciales de los atacantes.

#### Autenticación
- SSH proporciona una variedad de mecanismos de autenticación, incluyendo contraseñas, claves públicas y autenticación de dos factores. Esto ayuda a proteger su servidor de los atacantes que intentan adivinar contraseñas o utilizar exploits para obtener acceso.

#### Control de acceso
- SSH permite a los administradores de sistemas restringir el acceso a los usuarios autorizados. Esto ayuda a proteger su servidor de los atacantes.

---

## ¿Como proteger SSH?:
- Para proteger su servidor SSH, es importante seguir algunas prácticas recomendadas de seguridad. Aquí hay algunos consejos para configurar SSH más seguro:

### Cambiar el puerto por defecto
- El puerto por defecto para SSH es el 22. Este puerto es bien conocido por los atacantes, por lo que es una buena idea cambiarlo a un puerto más aleatorio. Puede cambiar el puerto en el archivo de configuración de SSH, que se encuentra en **/etc/ssh/sshd_config**.

#### Varios factores a considerar para cambiar a un buen puerto seguro:
- Seguridad: El puerto debe ser seguro y utilizar cifrado para proteger los datos.
- Disponibilidad: El puerto debe estar disponible para su uso sin causar problemas a otros servicios.
- Compatibilidad: El puerto debe ser compatible con los servicios que desea cambiar.

- Consejos para cambiar a un buen puerto seguro:
- Utilice un puerto seguro: Siempre que sea posible, utilice un puerto seguro para sus servicios. Esto ayudará a proteger sus datos de la interceptación.
- Elija un puerto disponible: Evite utilizar puertos que ya están en uso por otros servicios. Esto puede causar problemas de compatibilidad.
- Consulte la documentación del servicio: Consulte la documentación del servicio que desea cambiar para obtener información sobre los puertos compatibles.

#### Algunos ejemplos de puertos seguros que puede utilizar:
- Puerto 443: Puerto HTTPS para el protocolo HTTP
- Puerto 25: Puerto SSL para el protocolo SMTP
- Puerto 3306: Puerto SSL para el protocolo MySQL

---

### Deshabilitar el acceso root
- El acceso root a través de SSH debe deshabilitarse siempre que sea posible. Esto se debe a que el usuario root tiene acceso completo al sistema, lo que lo convierte en un objetivo atractivo para los atacantes. Puede deshabilitar el acceso root en el archivo de configuración de SSH, cambiando la línea `PermitRootLogin yes` a `PermitRootLogin no`.
```
PermitRootLogin no
```

---

### Deshabilitar el protocolo SSHv1
- El protocolo SSHv1 es un protocolo obsoleto que ya no es seguro. Los atacantes pueden explotar vulnerabilidades en SSHv1 para tomar el control de un servidor. Puede deshabilitar el protocolo SSHv1 en el archivo de configuración de SSH, cambiando la línea `Protocol 2` a `Protocol 2,1`.
```
Protocol 2

```

--- 

### Limitar el número de reintentos
- Los atacantes pueden intentar adivinar la contraseña de un usuario realizando múltiples intentos de conexión. Puede limitar el número de intentos de conexión en el archivo de configuración de SSH, cambiando la línea `MaxAuthTries` 6 a un número menor.
```
MaxAuthTries 3
```

---

### Limitar el número de sesiones
-- El límite de sesiones es el número máximo de sesiones SSH que un usuario puede tener abiertas al mismo tiempo. Si establece un límite de sesiones bajo, puede ayudar a proteger su servidor SSH de ataques de fuerza bruta, cambiando la línea `MaxSessions`a un número menor.

---

### Desactivar la autenticación por contraseña:
- La autenticación por contraseña es el método de autenticación predeterminado para SSH. Sin embargo, es el método menos seguro, ya que las contraseñas pueden ser adivinadas o robadas.
- Para aumentar la seguridad de su servidor SSH, puede desactivar la autenticación por contraseña. Esto obligará a todos los usuarios a utilizar la autenticación basada en claves, que es mucho más segura.
```
PasswordAuthentication no
```

---

### Habilitar la autenticación de dos factores
- La autenticación de dos factores (2FA) agrega una capa adicional de seguridad a SSH. Con 2FA, los usuarios deben proporcionar una contraseña y un código de verificación generado por un dispositivo 2FA, como un token de seguridad o una aplicación de autenticación. Puede habilitar la autenticación de dos factores en el archivo de configuración de SSH, cambiando la línea `UsePAM` a `UsePAM yes`.
```
UsePAMAuthtok yes
```

---

### Actualizar el software SSH
-- Los desarrolladores de SSH lanzan regularmente actualizaciones de seguridad para corregir vulnerabilidades conocidas. Es importante actualizar su software SSH a la última versión para mantenerse protegido de las últimas amenazas.
Permite que un usuario tenga un número ilimitado de sesiones SSH: MaxSessions unlimited

---

### Autenticación basada en claves:
- La autenticación basada en claves es un método de autenticación que utiliza un par de claves para identificar a un usuario. El par de claves consta de una clave privada y una clave pública. La clave privada se guarda en el dispositivo del usuario, mientras que la clave pública se almacena en el servidor.

- Para iniciar sesión, el usuario presenta su clave pública al servidor. El servidor utiliza la clave pública para generar una clave temporal. La clave temporal se compara con la clave privada del usuario. Si las dos claves coinciden, el usuario se autentica correctamente.

- La autenticación basada en claves es mucho más segura que la autenticación por contraseña. Las contraseñas pueden ser adivinadas o robadas, mientras que las claves privadas son mucho más difíciles de robar.

**Para generar un par de claves SSH:** ```ssh-keygen```
**Para copiar las cavles al usuario especifico en el servidor:** ```ssh-copy-id user2@192.168.1.1```

---

### Configurar la directiva LogLevel:

La directiva LogLevel se utiliza para controlar los tipos de mensajes que se envían al registro de errores. La directiva tiene un valor que indica el nivel de gravedad de los mensajes que se registrarán.

Los valores posibles para la directiva LogLevel son:

- **emerg**: Errores críticos que pueden causar que el servidor se detenga.
- **alert**: Errores que pueden causar daños o pérdida de datos.
- **crit**: Errores graves que pueden causar problemas en el servidor.
- **error**: Errores que pueden causar problemas en el servidor.
- **warn**: Advertencias que pueden indicar un problema potencial.
- **notice**: Información que puede ser útil para depurar o solucionar problemas.
- **info**: Información general sobre el funcionamiento del servidor.
- **debug**: Información detallada para fines de depuración.

Por defecto, la directiva LogLevel está configurada en warn. Esto significa que se registrarán los errores, las advertencias y las notificaciones.

**Para configurar `LogLevel` según tus necesidades:**

```
LogLevel debug  # Para registrar todos los mensajes, incluyendo mensajes de depuración.
LogLevel emerg  # Para registrar solo errores críticos.
LogLevel alert  # Para registrar solo errores graves.
LogLevel crit   # Para registrar solo errores generales.
LogLevel error  # Para registrar solo advertencias.
LogLevel warn   # Para registrar solo notificaciones.
LogLevel notice # Para registrar información útil para solución de problemas.
LogLevel info   # Para registrar información general del servidor.
```

---

### Restringir el acceso a los usuarios autorizados
- Al especificar los usuarios que pueden tener acceso al servidor SSH, puede restringir el acceso a los usuarios autorizados. Esto ayuda a proteger su servidor de los atacantes que intentan adivinar contraseñas o utilizar exploits para obtener acceso.

- Por ejemplo, para permitir que solo los usuarios user1 y user2 tengan acceso al servidor, puede agregar las siguientes líneas al archivo de configuración de SSH:
```
AllowUsers user1 user2
```

- También puede utilizar la directiva DenyUsers para especificar una lista de usuarios que no están autorizados a conectarse al servidor.

- Por ejemplo, para denegar el acceso a todos los usuarios excepto user1 y user2, puede agregar las siguientes líneas al archivo de configuración de SSH:
```
AllowUsers user1 user2
DenyUsers *
```

- Para configurar SSH para permitir solo conexiones desde una IP de origen específica, puede utilizar la directiva AllowFrom en el archivo de configuración de SSH. Esta directiva especifica una lista de direcciones IP que están autorizadas a conectarse al servidor.

- Por ejemplo, para permitir que solo las conexiones desde la dirección IP 192.168.1.1 tengan acceso al servidor, puede agregar la siguiente línea al archivo de configuración de SSH:
```
AllowFrom 192.168.1.1
```

- También puede utilizar la directiva DenyFrom para especificar una lista de direcciones IP que no están autorizadas a conectarse al servidor.

- Por ejemplo, para denegar el acceso a todas las conexiones excepto las de la dirección IP 192.168.1.1, puede agregar las siguientes líneas al archivo de configuración de SSH:
```
AllowFrom 192.168.1.1
DenyFrom *
```

- Para permitir que solo los usuarios con el nombre de usuario especifico y la dirección IP 192.168.1.1 tengan acceso al servidor, puede agregar la siguiente línea al archivo de configuración de SSH:
```
AllowUsers user1@192.168.1.1
```

- También puede utilizar la directiva DenyUsers para especificar una lista de usuarios que no están autorizados a conectarse al servidor.
```
AllowUsers user1@192.168.1.1 user2@192.168.1.1
DenyUsers *
```

---

##  Reinicie el servidor SSH para Guardar el archivo de configuración.
```
sudo systemctl restart sshd
```

---

## Para iniciar sesión en el servidor
```
ssh auser2@192.168.1.1
```

---

# Licencia
Este proyecto está bajo la licencia [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). Puedes compartir, adaptar y utilizar estos archivos siempre que des el crédito correspondiente al autor original.

# Nota importante
Se recomienda encarecidamente hacer una copia de seguridad de los datos importantes antes de continuar. El autor no se hace responsable de ningún daño o problema causado por el mal uso de estas tecnicas.
