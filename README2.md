Edge-Container-Tensorflow-ML-Model Using Google Cloud Shell -Readme 2
Reference: 
(a) [IGCP containers-gcs-tutorial](https://cloud.google.com/vision/automl/docs/containers-gcs-tutorial?hl=en_US) 

(b) [Github Automl Vision Predict](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/vision/automl/edge_container_predict)
(c) [Github Automl Edge Container Predict](https://raw.githubusercontent.com/GoogleCloudPlatform/python-docs-samples/master/vision/automl/edge_container_predict/automl_vision_edge_container_predict.py)
(d) [heartbeat.fritz.ai edge model on container](https://heartbeat.fritz.ai/automl-vision-edge-deploying-and-running-tensorflow-models-using-docker-containers-18336f78c4f7)
(e) [GCP Automl Vision - Github](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/vision/automl)

# Step 1: Download custom Automl object detection model with test-images and Automl scripts
```
    git clone https://github.com/mmmwembe/tensorflowjs-automl-container-edge.git
```

# Step 2 - Set environment variable for the Container Registry path and pull the Docker Vision AutoML Image
```
    export CPU_DOCKER_GCR_PATH=gcr.io/automl-vision-ondevice/gcloud-container-1.14.0:latest

    sudo docker pull ${CPU_DOCKER_GCR_PATH}

    docker image ls

```

# Step 3 - Create /tmp/mounted_model/0001 and copy saved_model.pb to this directory
```
 mkdir /tmp/mounted_model
 mkdir /tmp/mounted_model/0001
 sudo cp ./saved_model.pb /tmp/mounted_model/0001/

```

# Step 4 - Setup Container Name and Port number
```
export CONTAINER_NAME=automl_container
export PORT=8080

```

# Step 6: Run Container
```
sudo docker run --rm --name ${CONTAINER_NAME} -p ${PORT}:8501 -v "/tmp/mounted_model/0001":/tmp/mounted_model/0001 -t ${CPU_DOCKER_GCR_PATH}

```

# Step 7 - With the Container Running, Open another Terminal to run the python command
```
    cd tensorflowjs-automl-container-edge/

    python automl_vision_edge_container_predict.py --image_file_path=./test-image-01.jpg --image_key=1 --port_number=8080 

```

# Step 8 - Close Docker Container
```
    sudo docker stop ${CONTAINER_NAME}
```
