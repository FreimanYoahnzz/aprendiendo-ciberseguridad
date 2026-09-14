# Curso base para aprendizaje de ciberseguridad
Notas, apuntes y ejercicios del proceso de aprendizaje de ciberseguridad desde cero
En este repositorio se tendrá en cuenta el proceso desde cero para entrar en el mundo de la ciberseguridad, aprender sus fundamentos, aplicaciones y todo aquello a lo cual se aplique, la meta es aprender todo lo que se pueda para ser el mejor en ello.

## Contenido
- Apuntes y notas de los temas que se van estudiando
- Ejercicios y retos resueltos
- Certificaciones en progreso

## Fase 1: Fundamentos técnicos
1. [Redes: modelo TCP/IP y OSI, direccionamiento IP y subnetting, DNS, DHCP, HTTP/HTTPS, protocolos comunes (FTP, SSH, SMTP), firewalls básicos
2. Sistemas Linux: terminal, sistema de archivos, permisos, gestión de usuarios, procesos, administración básica de servicios
3. Sistemas Windows: administración básica, Active Directory
4. Programación aplicada a seguridad: python (automatización, parsing de logs, herramientas propias)

   
## Fase 2: Conceptos centrales de seguridad
5. Tríada CIA, gestión de riesgo, modelos de amenazas
6. Criptografía (hashing, cifrado simétrico/asimétrico, certificados, TLS)
7. Autenticación y control de acceso (MFA, SSO, gestión de identidades)
8. Tipos de ataques y vectores (phishing, malware, ingeniería social, ataques de red)

   
## Fase 3: Seguridad ofensiva(Red Team / Pentesting)
9. Metodología de pentesting (reconocimiento, escaneo, explotación, post-explotación, reporte)
10. Herramientas: Nmap, Burp Suite, Metasploit, Wireshark
11. Seguridad web: OWASP Top 10 a fondo (inyección SQL, XSS, CSRF, etc.) con PortSwigger Web Security Academy 
12. Práctica constante en TryHackMe y HackTheBox
## Fase 4: Seguridad defenciva(Blue Team / SOC)
13. Monitoreo y detección: SIEM, logs, IDS/IPS
14. Respuesta a incidentes
15. Hardening de sistemas
16. Análisis de malware (introducción)

    
## Fase 5: Especialización(Elegir a lo que le apuntes y más te guste)
17. Cloud security (AWS/Azure)
18. Seguridad de aplicaciones (AppSec)
19. Forense digital
20. GRC (Governance, Risk & Compliance) enfocado más al interés de la gestión y lo normativo


## Certificaciones
algunas se irán integrando a lo largo del curso
- CompTIA Security+ → después de Fase 1 y 2
- eJPT → al terminar Fase 3 básica, certificación práctica de pentesting junior
- CompTIA CySA+ o similar, para quien se incline por el Blue Team
- OSCP → objetivo a mediano-largo plazo, la más respetada en pentesting, y que exige nivel real

# Fase 1
## 1. Redes
Para entrar al mundo de la ciberseguridad, primero hay que entender Redes, ya que casi todo lo que hace un profesional en ciberseguridad pasa por entender 
como viaja la información entre un computador y otro. Si no se entiende esto desde el principio, no se sabrá entender el lenguaje en el cual se comunican las
dos maquinas, y por ende lo único que se hará es usar las herramientas de seguridad a ciegas, sin tener la menor idea de que es lo que se esta viendo,
atacando o defendiendo.

 **¿Qué es una red?**  
Una red es básicamente un grupo de dispositivos conectados entre que pueden intercambiar información. Estas pueden ser relativamente pequeñas, desde un simple
computador computador conectado a un router, ó tan grandes como todo internet.

Para que dos maquinas(computadores) se entiendan, estas necesitan hablar el mismo idioma, para esto se utilizan unos protocolos, los cuales son 
un conjunto de reglas y normas estandarizadas que definen como se deben transferir, cifrar, autenticar, y verificar los datos entre los sistemas, para 
protegerlos de ataques cibernéticos. Antes de ver estos protocolos hay que saber como se organizan.

- **Modelo TCP/IP**  
Para entender este modelo, imaginemos que enviar información por internet es como enviar una carta, no vasta con solo enviar el mensaje, también se necesita saber 
la dirección, un mensajero que la lleve de la forma correcta al destino a la que quiere ser enviada y que esta llegue completa y en orden. Para hacer esto en una red
existe el modelo TCP/IP, el cual organiza la información por capas(bloques) y se asegura que la información llegue completa a su destino. Este modelo se divide en 
dos protocolos:

    - **Internet Protocol**(Protocolo de internet) más conocido como **IP**, se encarga de ponerle una dirección a cada dispositivo que este conectado a una red, y decide 
   el camino que debe de seguir la información para llegar de un dispositivo a otro.
   
      En palabras simples es como cuando se hace algún tipo de pedido por internet, para que el paquete llegue a su destino se debe dar una la dirección, cada casa tiene una
      dirección única(calle, numero, ciudad), para que el paquete sea entregado correctamente, el transportador debe conocer dicha información para saber el destino  del
      paquete y poder entregarlo. Eso mismo pasa en una red, cada dispositivo conectado a esa red tiene una dirección IP única para que otros dispositivos sepan a donde
      enviarle la información.
   
   - **Transmission Control Protocol**(Protocolo de Control de Transmisión), más conocido como **TCP**, se encarga de que la información enviada a esa IP llegue de forma
   completa, en orden y sin errores.
   
      Cuando se envía información grande por internet como una pagina web completa, esta no viaja en una sola pieza, se empaqueta en módulos(paquetes pequeños),
      cada uno de estos módulos viajan por separado, a veces incluso lo hacen por rutas distintas dentro de la red. El TCP es el encargado numerar dichos módulos para que el 
      receptor sepa en que orden armarlos de nuevo, confirmar que cada paquete llegue bien, y en caso de que algunos de los módulos se pierdan en el camino, el TCP pide que se le reenvíen
      para organizar la información y así entregarla de forma completa y en el orden correcto a quien pidió la información.

  Teniendo lo mencionado anteriormente en cuenta, como la IP es una cantidad determinada de números separados por puntos tales como: "142.250.190.78" ó "192.168.1.", y al ser tan largos,
  seria muy tedioso tener que memorizarse una IP diferente para cada pagina a la cual se quisiera acceder.

  Para resolver ese problema existe el **Domain Name System**(Sistema de Nombres de Dominio) conocido como **DNS**, el cual actúa como una agenda de contactos de un teléfono celular, en donde
  la persona no tiene que saber necesariamente el número de teléfono de una persona en especifico para contactarla, si no que accede a dicho contacto por medio de su nombre. Ese nombre cuando
  se registra queda asociado a el número de teléfono correspondiente, entonces cuando se quiere contactar a dicha persona, internamente busca el número asociado a ese nombre para así proceder a
  contactarla.

  El DNS hace exactamente lo mismo, pero para internet, se escribe el nombre de la pagina que se desea buscar, por ejemplo "google.com", y el DNS busca la dirección IP asociada a esa pagina.
   
  **¿Cómo funciona el proceso de "Buscar"?**
  Cuando se escribe "google.com", el computador le pregunta a un servidor DNS que normalmente es el del proveedor de internet, o uno público algo como: "oye, ¿cuál es la dirección
  IP de google.com?". El servidor DNS responde con la IP correcta, y ahí recién empieza el proceso de conexión TCP, envío de paquetes, etc.
   
  


