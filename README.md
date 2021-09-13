# skaffold-demo
Skaffold 101 Demo with Getting Started Example, configured to work with GCP : GKE and GCR.

# Tools used
* Google Cloud Shell : It comes with Docker, Kubernetes Tools (kubectl, kubectx), Skaffold installed. Free of cost for anyone with Google Account. 
* Google Container Registry : For pushing the artifacts (Container Images) from above. 
* Google Kubernetes Engine : Demo cluster to show the Pods being deployed and the Skaffold workflow.

# Configuration Needed
Create a GKE cluster. Go with default configuration. Restrict it to just one node and select a lower N1 Machine type. 
* Note down the project id. Let’s call it ```%GCP_PROJECT_ID%```
* Note down the Zone. Let’s call it ```%GCP_PROJECT_ZONE%```
* Note down the Cluster Name. Let’s call it ```%CLUSTER_NAME%```

A ```kubecfg``` entry needs to be created for this cluster and is added via the following command:

```$ gcloud container clusters get-credentials %CLUSTER_NAME% --zone=%GCP_PROJECT_ZONE%```


Validate that the ```kubectx``` shows the list of clusters that have been configured and note down the default cluster that it is pointing to. 

Alternatively run ```kubectx -c``` to get the default cluster. 

If it is not the default one, use the following command to set the default cluster : ```$ kubectx context-name```


Set the default registry for Skaffold to Google Container Registry via the following command:

```$ skaffold config set default-repo gcr.io/%GCP_PROJECT_ID%```

Confirm that Skaffold is now pointing to both the remote Google Container Registry and the GKE Cluster via the following command:

```$ skaffold config list```

# Demonstrate couple of the End-To-End Pipelines:
```$ skaffold run```
```$ skaffold dev```

* While demonstrating ```skaffold dev``` , let the pipeline complete. Visit GCR, GKE to show the image artifact and Kubernetes Artifacts being created and ready.
* Then go to main.go file and make a code change. 
* Come back to the skaffold dev console and show the files being compiled again and deployed. 

* Demonstrate other Pipeline building blocks for CI/CD:
```$ skaffold build ```
```$ skaffold build --file-output=tags.json```
```$ skaffold deploy --build-artifacts=tags.json```

One step for above: 
```$ skaffold build -q | skaffold deploy --build-artifacts -```



