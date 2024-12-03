
Cosmocloud Deploy Helm Chart
============================

This Helm chart deploys a backend service, a frontend service, and a Redis database.

Features:
---------
- Backend: Uses image `shreybatra/sample-backend`. Exposed on port 8000 via ClusterIP.
- Frontend: Uses image `shreybatra/sample-frontend`. Exposed on port 5175 via NodePort.
- Redis: Uses official `redis` image. Exposed on port 6379 via ClusterIP.

Installation:
-------------
1. Clone the repo:
   git clone https://github.com/anujtomar1/cosmocloud-deploy.git
   cd cosmocloud-deploy
2. Install the chart:
   helm install testapp cosmocloud-deploy --atomic --timeout 30s

Configuration:
--------------
The `values.yaml` file contains the default configurations:
- `replicaCount`: Number of replicas for each service (default: 1).
- `backend.image`: Docker image for the backend service.
- `frontend.image`: Docker image for the frontend service.
- `redis.image`: Docker image for Redis.

Code Explanation:
-----------------
1. **Backend Deployment (backend-deployment.yaml)**:
   - Deploys the backend using the `shreybatra/sample-backend` image.
   - Sets `REDIS_URI` to `redis://redis-svc:6379` for backend-redis communication.

2. **Frontend Deployment (frontend-deployment.yaml)**:
   - Deploys the frontend using the `shreybatra/sample-frontend` image.
   - Sets `BACKEND_URL` to `http://backend-svc:8000` for frontend-backend communication.

3. **Redis Deployment (redis-deployment.yaml)**:
   - Deploys Redis using the official `redis` image.

4. **Services**:
   - **Backend Service (backend-service.yaml)**: ClusterIP on port 8000.
   - **Frontend Service (frontend-service.yaml)**: NodePort on port 5175 (NodePort 31000).
   - **Redis Service (redis-service.yaml)**: ClusterIP on port 6379.

Testing and Cleanup:
--------------------
To uninstall the application:
- helm uninstall testapp


