The directory `services` contains basic kubernetes resource files for MySQL, Apache Kafka, MySQL and Prometheus for use in development.  The directory `server` contains a Kustomize based directory structure with `dev` and `prod` profiles.  The `dev` profile is configured for use with the resources created in the `services` directory.

`kapp` is a simple deployment tool focused on the concept of a "Kubernetes application" — a set of resources with the same label.  We will install the development services using `kapp`

```
kapp -y deploy -a mysql -f ./services/mysql
```

To uninstall use `kapp delete -a mysql`.

To deploy the Skipper Server in the dev profile

```
kubectl kustomize ./skipper-server/kustomize/overlays/dev | kapp -y deploy -a skipper-server -f -
```

To uninstall use `kapp -y delete -a skipper-server`


To deploy the Data Flow Server in the dev profile

```
kubectl kustomize ./data-flow-server/kustomize/overlays/dev | kapp -y deploy -a data-flow-server -f -
```

To uninstall use `kapp -y delete -a data-flow-server`
