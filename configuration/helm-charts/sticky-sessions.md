# Sticky sessions

if you're running more than one pod and have authentication enabled you will encounter issues with sessions, as we store them in cookies and other instances are not aware of your sessions.

The solution for this would be using sticky session/session affinity.

An example:

```
    nginx.ingress.kubernetes.io/affinity: cookie
    nginx.ingress.kubernetes.io/affinity-mode: balanced
    nginx.ingress.kubernetes.io/session-cookie-expires: "172800"
    nginx.ingress.kubernetes.io/session-cookie-max-age: "172800"
    nginx.ingress.kubernetes.io/session-cookie-name: kafka-ui
```
