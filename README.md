{  "log": {
    "access": "",    "error": "",
    "loglevel": "warning"  },
  "inbounds": [    {
      "tag": "socks",      "port": 10808,
      "listen": "127.0.0.1",      "protocol": "socks",
      "sniffing": {        "enabled": true,
        "destOverride": [          "http",
          "tls"        ],
        "routeOnly": false
      },      "settings": {
        "auth": "noauth",        "udp": true,
        "allowTransparent": false
      }    },
    {      "tag": "http",
      "port": 10809,      "listen": "127.0.0.1",
      "protocol": "http",      "sniffing": {
        "enabled": true,        "destOverride": [
          "http",          "tls"
        ],        "routeOnly": false
      },      "settings": {
        "auth": "noauth",        "udp": true,
        "allowTransparent": false      }
    }  ],
  "outbounds": [    {
      "tag": "proxy",      "protocol": "vless",
      "settings": {        "vnext": [
          {            "address": "zula.ir",
            "port": 443,            "users": [
              {                "id": "a41d3936-89ac-4156-8e5b-c6af8e0e2e75",
                "alterId": 0,                "email": "t@t.tt",
                "security": "auto",                "encryption": "none",
                "flow": ""              }
            ]          }
        ]      },
      "streamSettings": {        "network": "ws",
        "security": "tls",        "tlsSettings": {
          "allowInsecure": true,          "serverName": "paRiSArGO.TARAhiviP.SitE",
          "alpn": [            "h2",
            "http/1.1"          ],
          "fingerprint": "chrome",          "show": false
        },        "wsSettings": {
          "path": "/c7884e79-6dc2-4a58-8de1-1e0bb968f177?ed=2048",          "headers": {
            "Host": "paRiSArGO.TARAhiviP.SitE"          }
        },        "sockopt": {
          "dialerProxy": "fragment",          "tcpKeepAliveIdle": 100,
          "mark": 255,          "tcpNoDelay": true
        }      },
      "mux": {        "enabled": true,
        "concurrency": 8      }
    },    {
      "tag": "fragment",      "protocol": "freedom",
      "settings": {
        "domainStrategy": "AsIs",        "fragment": {
          "packets": "tlshello",          "length": "10-15",
          "interval": "20-40"        }
      },      "streamSettings": {
        "sockopt": {          "tcpNoDelay": true,
          "tcpKeepAliveIdle": 100        }
      }    },
    {      "tag": "direct",
      "protocol": "freedom",      "settings": {}
    },    {
      "tag": "block",
      "protocol": "blackhole",      "settings": {
        "response": {          "type": "http"
        }      }
    }  ],
  "routing": {    "domainStrategy": "AsIs",
    "rules": [      {
        "type": "field",        "inboundTag": [
          "api"        ],
        "outboundTag": "api",        "enabled": true
      },      {
        "id": "5465425548310166497",        "type": "field",
        "outboundTag": "direct",        "domain": [
          "domain:ir",          "geosite:cn"
        ],        "enabled": true
      },      {
        "id": "5425034033205580637",        "type": "field",
        "outboundTag": "direct",        "ip": [
          "geoip:private",          "geoip:cn",
          "geoip:ir"        ],
        "enabled": true      },
      {        "id": "5627785659655799759",
        "type": "field",        "port": "0-65535",
        "outboundTag": "proxy",        "enabled": true
      }    ]
  }}
