# Python Application Deployment on Kubernetes

## Overview
This project contains a Python application that is deployed on Kubernetes. The deployment is managed using a Kubernetes configuration file (`k-8.yml`) and is designed to scale automatically based on demand using a Horizontal Pod Autoscaler (`hpa.yml`).

## Files
- **k-8.yml**: Contains the configuration for the Kubernetes deployment and service for the Python application. It defines the deployment specifications, including the number of replicas, container image, ports, and environment variables.
  
- **hpa.yml**: This file contains the Horizontal Pod Autoscaler configuration for the Python application deployment. It specifies the target deployment, metrics for scaling, and the minimum and maximum number of replicas.

## Setup Instructions
1. Ensure you have a Kubernetes cluster running.
2. Apply the deployment configuration:
   ```
   kubectl apply -f k-8.yml
   ```
3. Apply the Horizontal Pod Autoscaler configuration:
   ```
   kubectl apply -f hpa.yml
   ```
4. Verify that the deployment and service are running:
   ```
   kubectl get deployments
   kubectl get services
   ```
5. Monitor the Horizontal Pod Autoscaler:
   ```
   kubectl get hpa
   ```

## Usage
Once the application is deployed, you can access it through the service defined in `k-8.yml`. The application will automatically scale based on the defined metrics in the Horizontal Pod Autoscaler.