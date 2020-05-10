Edge-Container-Tensorflow-ML-Model
Reference: 
(a) https://cloud.google.com/vision/automl/docs/containers-gcs-tutorial?hl=en_US
(b) https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/vision/automl/edge_container_predict


# Step 1: Download AutoML pb model from GCP Storage
```
gsutil cp -r gs://cards-automl-results-bucket/container-model/model-export/iod/tf_saved_model-cards_automl_model-2020-05-09T10:41:58.203Z/* ./
```

# Step 2: Use Netron to check that the model is good


# Step 3: Check that Docker is installed (if not installed, install Docker)
```
    docker --version
    docker run hello-world
```

# Step 4: Set environment variable for the Container Registry path and pull the Docker Vision AutoML Image
```
    set CPU_DOCKER_GCR_PATH=gcr.io/automl-vision-ondevice/gcloud-container-1.14.0:latest

    docker pull ${CPU_DOCKER_GCR_PATH}

    docker pull gcr.io/automl-vision-ondevice/gcloud-container-1.14.0:latest

```

# Step 5: List Docker Images
```
    docker image ls
```

# Step 6: 