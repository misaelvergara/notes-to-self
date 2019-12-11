## WEB SERVER
Web servers are computers that deliver web pages. Every web server has an **IP address** and a **domain name**.
Web servers fetches a page and sends it as a response.
Turning a computer into a web server requires the use of softwares which serves this purpose.

Accessing a web page generates a request that leaves your **local area network** (HTTP GET REQUEST), travels to the **global area network** until it reaches a computer, which is the server that serves you a web page (response containing the content of the page).

```mermaid
graph LR
A(COMPUTER) --REQUEST--> B(LAN) 
B --> C(GAN)
C --> D(SERVER)
D --RESPONSE--> C
C --> B
B --> A
```
## NGINX
### ARCHITECTURE
Nginx uses master-slave architecture by supporting event-drive, asynchronous and non-blocking model.


<!--stackedit_data:
eyJoaXN0b3J5IjpbMzAzNzkyNDhdfQ==
-->