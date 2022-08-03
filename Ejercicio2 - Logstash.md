# Ejercicio 2 - Logstash

Objetivo: Se desea recoger información de diferentes fuentes, aplicarle las transformaciones necesarias y mandarlo a tres servidores HTTP. Dos de los servidores serán dedicados a una fuente especifica, y el tercero recibirá información de las dos fuentes. 

### Requisitos: 
- El servidor HTTP1 solamente podrá recibir mensajes que presenten la estructura A.
- El servidor HTTP2 solamente podrá recibir mensajes que presenten la estructura B.
- El servidor HTTP3 solamente podrá recibir mensajes que presenten la estructura C y D.

### Tips:
- Filtros a tener en cuenta: prune, rename, grok, add_field...
- _Fuente 1_: Ficheros de log.
- _Fuente 2_: Disponibilidad de los sistemas y servicios involucrados.

#### Estructuras

Estructura A:
```
{
    "@version": "1",
    "@timestamp": "2022-07-20T10:31:00.886Z",
    "ip": "195.236.141.3",
    "date_type": "log",
    "source": "ej2-filebeat",
    "tags": [
        ...
    ],
    "user": "wolff2267",
    "hostname": "ej2-filebeat",
    "syslog_message": "[20/Jul/2022:10:30:59 +0000] \"GET /holistic HTTP/1.0\" 201 12449",
    "msg": "195.236.141.3 - wolff2267 [20/Jul/2022:10:30:59 +0000] \"GET /holistic HTTP/1.0\" 201 12449"
}
```

Estructura B:
```
{
    "@version": "1",
    "@timestamp": "2022-07-20T10:31:30.438Z",
    "hostname": "ej2-filebeat",
    "date_type": "ping",
    "source": "ej2-heartbeat",
    "tags": [
        ...
    ],
    "msg": {
        "ip": "192.168.112.2",
        "name": "PingRequest",
        "id": "ping-request-c44ec252ea325e8a",
        "check_group": "1b586097-0817-11ed-b7bc-0242c0a87008",
        "status": "up",
        "timespan": {
            "lt": "2022-07-20T10:31:35.440Z",
            "gte": "2022-07-20T10:31:30.440Z"
        },
        "type": "icmp",
        "duration": {
            "us": 1392
        }
    }
}
```

Estructura C:
```
{
    "@version": "1",
    "@timestamp": "2022-07-20T10:31:25.992Z",
    "hostname": "ej2-filebeat",
    "date_type": "log",
    "source": "ej2-filebeat",
    "tags": [
        ...
    ],
    "msg": "9.132.243.234 - heller6428 [20/Jul/2022:10:31:24 +0000] \"DELETE /platforms/synergize HTTP/1.1\" 503 12863"
}
```

Estructura D:
```
{
    "@version": "1",
    "@timestamp": "2022-07-20T10:31:00.434Z",
    "hostname": "ej2-logstash",
    "date_type": "ping",
    "source": "ej2-heartbeat",
    "tags": [
        ...
    ],
    "msg": {
        "ip": "192.168.112.6",
        "name": "PingRequest",
        "id": "ping-request-83e1a4560c5e37a5",
        "check_group": "09760263-0817-11ed-b7bc-0242c0a87008",
        "status": "up",
        "type": "icmp",
        "duration": 361
    }
}
```


