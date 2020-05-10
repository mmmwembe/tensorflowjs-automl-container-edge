Edge-Container-Tensorflow-ML-Model
Reference: 
(a) https://cloud.google.com/vision/automl/docs/containers-gcs-tutorial?hl=en_US
(b) https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/vision/automl/edge_container_predict
(c) https://raw.githubusercontent.com/GoogleCloudPlatform/python-docs-samples/master/vision/automl/edge_container_predict/automl_vision_edge_container_predict.py
(d) https://heartbeat.fritz.ai/automl-vision-edge-deploying-and-running-tensorflow-models-using-docker-containers-18336f78c4f7
(e) https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/vision/automl

--------

Best starting point: 
```
git clone https://github.com/mmmwembe/tensorflowjs-automl-container-edge.git

```
--------


# Step 1: Download AutoML pb model from GCP Storage (if not already in git repo)
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

    // docker pull gcr.io/automl-vision-ondevice/gcloud-container-1.14.0:latest

   docker image ls
```

# Step 5: Copy saved_model.pb to '/tmp/mounted_model/0001'
```
 sudo  cp .saved_model.pb /tmp/mounted_model/0001/
 
```

# Step 6: Setup Container Name and Port number

${CONTAINER_NAME} - A string indicating the container name when it runs, for example CONTAINER_NAME=automl_container
${PORT} - A number indicating the port in your device to accept REST API calls later, such as PORT=8080
```
export CONTAINER_NAME=automl_container
export PORT=8080

```
# Step 7: Run Container
```
sudo docker run --rm --name ${CONTAINER_NAME} -p ${PORT}:8501 -v "/tmp/mounted_model/0001":/tmp/mounted_model/0001 -t ${CPU_DOCKER_GCR_PATH}

```

# Step 8 - With the Container Running, Open another Terminal to run the python command
```
    python automl_vision_edge_container_predict.py \
    --image_file_path=./test-images/test-image-01.jpg --image_key=1 --port_number=8051
```

# Step 9 - Close Docker Container
```
    sudo docker stop ${CONTAINER_NAME}
```