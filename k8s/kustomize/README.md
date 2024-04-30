

# Kustomize simple example

    .
    ├── base  
    │   ├── kustomization.yaml  
    │   └── pod-1.yaml  
    ├── overlays  
    │   └── dev  
    │       ├── kustomization.yaml  
    │       └── pod-1-dev.yaml  
    └── README.md  


Original pod-1-dev.yml file

    apiVersion: v1
    kind: Pod
    metadata:
      name: pod-1
      labels:
        app: primeiro-pod
    spec: 
      containers:
        - name: container-pod-1
          image: nginx:stable
          ports:
            - containerPort: 80

overlays/dev/kustomization.yaml file define somes changes  

    commonLabels:
      env: dev
      
    nameSuffix: -dev

Kustomize command  
`$ kubectl kustomize overlays/dev/`

Result (env label included and name changed)

    apiVersion: v1
    kind: Pod
    metadata:
      labels:
        app: primeiro-pod
        env: dev
      name: pod-1-dev
    spec:
      containers:
      - image: nginx:stable
        name: container-pod-1
        ports:
        - containerPort: 80
