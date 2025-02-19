# KitOps Notes

## Quickstarts

Podman example

```sh
podman run -it --rm -p 8080:8000 "jozu.ml/jozu/llama3-8b/llama-cpp:8B-instruct-q5_0"
```

Easy deploy of `llama3-8b` on OpenShift

```sh
oc new-project models

oc new-app \
  --name llama3-8b \
  --image jozu.ml/jozu/llama3-8b/llama-cpp:8B-instruct-q5_0

oc expose deployment/llama3-8b \
  -l app=llama3-8b \
  --port=8000

oc expose service/llama3-8b \
  -l app=llama3-8b

oc patch route/llama3-8b --type merge \
  -p '{"spec": {"tls": {"termination": "edge", "insecureEdgeTerminationPolicy": "Redirect"}}}'
```

Some basic commands around `kit`

```sh
# storage is at ~/.local/share/kitops
kit pull jozu.ml/jozu/llama3-8b:8B-text-q8_0

# list models in local storage
kit list

# display info of model
kit info jozu.ml/jozu/llama3-8b:8B-text-q8_0

# unpack a model into a folder < scratch >
kit unpack jozu.ml/jozu/llama3-8b:8B-text-q8_0 -d scratch
```

Explore OCI artifacts created by `kit`

```sh
oras copy jozu.ml/jozu/llama3-8b:8B-text-q8_0 --to-oci-layout scratch/
```

## Links

- https://kitops.org
- https://github.com/jozu-ai/kitops
- https://jozu.ml/docs/understanding-jozu-hub/modelkit-containers.html
- https://jozu.ml/repository/jozu/llama3-8b/8B-instruct-q5_0/deploy
- https://github.com/oras-project/oras
- https://github.com/containers/omlmd
- https://containers.github.io/omlmd
- https://github.com/meta-llama/llama-stack/blob/main/llama_stack/providers/utils/inference/model_registry.py
