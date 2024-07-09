# Dash app deployed on Openshift Local
## Start Openshift Local
`crc start`
## Run the helm command to deploy postgres
`helm upgrade postgres ./postgres-minimal --create-namespace --install --atomic \
--namespace starlake-dash \
--set storageClass=crc-csi-hostpath-provisioner \
--set image=bitnami/postgresql:16.1.0-debian-11-r0`
## Run the helm command to deploy the push script
`helm upgrade push-script ./push-script --create-namespace --install --atomic --namespace starlake-dash`
## Can uninstall the push script container after it has finished pushing
`helm uninstall push-script -n starlake-dash`
## Run the helm command to deploy the pgadmin *Optional
`helm uninstall push-script -n starlake-dash`
## Run the helm command to deploy the pgadmin *Optional
`helm upgrade pgadmin ./pgadmin-minimal -n starlake-dash --create-namespace --install --atomic \
--set storageClass=crc-csi-hostpath-provisioner \
--set route.tls.enabled=true`
## Run the helm command to deploy the dash application
`helm upgrade dash-app ./dash-app/ --create-namespace --install --atomic --namespace starlake-dash`
## Port forward the port that the application runs at
`oc port-forward svc/dash-app 8050:8050 -n starlake-dash`
## Access at localhost 127.0.0.1:8050
