Create a middleware:

```yaml
apiVersion: traefik.containo.us/v1alpha1
kind: Middleware
metadata:
    name: authentik
spec:
    forwardAuth:
        address: http://outpost.company:9000/outpost.goauthentik.io/auth/traefik
        trustForwardHeader: true
        authResponseHeaders:
            - X-authentik-username
            - X-authentik-groups
            - X-authentik-email
            - X-authentik-name
            - X-authentik-uid
            - X-authentik-jwt
            - X-authentik-meta-jwks
            - X-authentik-meta-outpost
            - X-authentik-meta-provider
            - X-authentik-meta-app
            - X-authentik-meta-version
```

Add the following settings to your IngressRoute

By default traefik does not allow cross-namespace references for middlewares:

See [here](https://doc.traefik.io/traefik/v2.4/providers/kubernetes-crd/#allowcrossnamespace) to enable it.

```yaml
spec:
    routes:
        - kind: Rule
          match: "Host(`app.company`)"
          middlewares:
              - name: authentik
                namespace: authentik
          priority: 10
          services: # Unchanged
```
