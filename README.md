### Tip: UUID recommends using UUID generator, Google it: UUID generation. . . . If you cannot connect, 80% of the UUID does not meet the requirements! !

### Reminder: Misuse may cause the account to be deleted! ! !

### The following content is modified according to the original author's project description, so that beginners can understand it easily!

### Detailed video tutorial YouTube: https://youtu.be/dE730hVgmUs
   
* The original author's Heroku script is a multi-protocol coexistence script. This project uses [xray](https://github.com/XTLS/Xray-core)+caddy, and deploys vmess vless trojan-go shadowsocks socks via ws transmission mode at the same time For other protocols, the camouflage website has been configured by default.

## Server creation operation process
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/YG-tsj/ Heroku-xray-trojangows-ssws)
Click the purple `Deploy to Heroku` above, it will jump to the heroku app creation page, fill in the application name, select the node (US or Europe), custom UUID code, other suggestions keep the default, click below deploy, and it will be done in a few seconds !

## vmess vless trojan-go shadowsocks corresponds to the client parameters of the reference as follows, the content with () at the end is only a reminder

## 1: Xray

### Proxy agreement: vless+ws+tls or vmess+ws+tls
* Server address: optional ip (eg: icook.tw)
* Port: 443
* Default UUID: 8f91b6a0-e8ee-11ea-adc1-0242ac120002 (must customize the UUID code when creating)
* Encryption: none
* Transmission protocol: ws
* Camouflage type: none
* Disguise host: ****.workers.dev (CF Workers anti-generation address)
* SNI address: ****.workers.dev (CF Workers anti-generation address)
* path: /custom UUID code-vless or /custom UUID code-vmess (note: there is a slash / before it)
* vmess additional id (alterid): 0
* Underlying transmission security: tls
* Skip certificate verification: false

## 2: Trojan-Go+ws

* Server address: optional ip (eg: icook.tw)
* Port: 443
* Password: 8f91b6a0-e8ee-11ea-adc1-0242ac120002 (must customize the UUID code when creating)
* Transmission protocol: ws
* Path: /Custom UUID code -trojan (note: there is a slash /)
* SNI address: ****.workers.dev (CF Workers anti-generation address)
* Disguise host: ****.workers.dev (CF Workers anti-generation address)

## 3: Shadowsocks+ws+tls

* Server address: application name.herokuapp.com
* Port: 443
* Password: 8f91b6a0-e8ee-11ea-adc1-0242ac120002 (must customize the UUID code when creating)
* Encryption: chacha20-ietf-poly1305
* Plug-in options: tls;host=application name.herokuapp.com;path=/custom UUID code-ss


### CloudFlare Workers anti-generation code (supports WS mode of VLESS\VMESS\Trojan-Go, can use the application names of two accounts (UUID and path are the same), and execute separately on the single and double number days. 550+550 hours)

```
const SingleDay ='application name 1.herokuapp.com'
const DoubleDay ='application name 2.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
### Original author project address: https://github.com/mixool/xrayku
