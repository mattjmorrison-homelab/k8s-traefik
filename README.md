# homelab-traefik

Configuration overrides for k3s's built-in Traefik, managed via ArgoCD.

k3s deploys Traefik itself via an internal `HelmChart` resource (`traefik`, in `kube-system`) rather than through ArgoCD directly. The supported way to customize it without replacing k3s's own management of it is a `HelmChartConfig` resource with the same name/namespace — k3s's helm-controller merges its `valuesContent` into the chart install.

`manifests/helmchartconfig.yaml` configures the `web` entrypoint (port 80) to permanently redirect all plain HTTP traffic to the `websecure` entrypoint (port 443) — so every `*.morrisons.site` service gets HTTPS-only access automatically, once [homelab-cert-manager](https://github.com/mattjmorrison/homelab-cert-manager) has a certificate in place.

---

[Homelab Docs](https://github.com/mattjmorrison/homelab/blob/main/docs/INDEX.md)
