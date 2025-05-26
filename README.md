# k8s-learning
k8s-demo


## DockerFile

```Dockerfile
FROM openjdk:8
COPY *.jar /app.jar
CMD ["--spring.profiles.active=prod"]
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app.jar"]
```

## Build Image
```sh
docker build -t testdemo:1.0.0 .
```

## Create configmap
```sh
mkdir configmap
mv application-prod.properties configmap/
kubectl create configmap test-config --from-file=configmap
```

## Edit k8s yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-demo
spec:
  containers:
    - name: test-container
      image: testdemo:1.0.0
      volumeMounts:
      - name: config-volume
        mountPath: /config
  volumes:
    - name: config-volume
      configMap:
        name: test-config
  restartPolicy: Never
```

## Run pod

```sh
kubectl create -f k8s.yaml
```
