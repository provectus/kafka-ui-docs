# SSL example

## Implement ssl for kafka-ui

To implement SSL for kafka-ui you need to provide JKS files into the pod. Here is the instruction on how to do that.

### Create config map with content from kafka.truststore.jks and kafka.keystore.jks.

To create configmap use following command.\


```
kubectl create configmap ssl-files --from-file=kafka.truststore.jks --from-file=kafka.keystore.jks
```

If you have specified namespace use command.\


```
kubectl create configmap ssl-files --from-file=kafka.truststore.jks --from-file=kafka.keystore.jks -n {{namespace}
```



### Create secret.

Encode secret with base64(You can use this tool https://www.base64encode.org/). Create secret.yaml file with the following content

```
apiVersion: v1
kind: Secret
metadata:
 name: ssl-secret
 # Specify namespace if needed, uncomment next line and provide namespace
 #namespace: {namespace}
type: Opaque
data:
 KAFKA_CLUSTERS_0_PROPERTIES_SSL_TRUSTSTORE_PASSWORD: ##Base 64 encoded secret
 KAFKA_CLUSTERS_0_PROPERTIES_SSL_KEYSTORE_PASSWORD: ##Base 64 encoded secret
```

### Create ssl-values.yaml file with the following content.

```
existingSecret: "ssl-files"


env:
- name:  KAFKA_CLUSTERS_0_PROPERTIES_SSL_TRUSTSTORE_LOCATION 
  value:  /ssl/kafka.truststore.jks
- name: KAFKA_CLUSTERS_0_PROPERTIES_SSL_KEYSTORE_LOCATION
  value: /ssl/kafka.keystore.jks


volumeMounts:
 - name: config-volume
   mountPath: /ssl

volumes:
 - name: config-volume
   configMap:
     name: ssl-files
```

### Install chart with command

```
helm install kafka-ui kafka-ui/kafka-ui-charts -f ssl-values.yaml
```

If you have specified namespace for configmap and secret please use this command

```
helm install kafka-ui kafka-ui/kafka-ui -f ssl-values.yaml -n {namespace}
```
