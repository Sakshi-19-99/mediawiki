# mediawiki
MediaWiki Deployment on Kubernetes using Helm
This repository includes guidelines and config files for setting up MediaWiki on Kubernetes with the help of Helm. 

Pre-requisites
1. Installed Kubernetes
2. Installed Helm
3. Installed Azure CLI

Installation Steps:
Steps to deploy MediaWiki on Kubernetes:
1. Clone the repository
2. Log in to azure account
3. Create resource group and aks cluster
4. Deploy MediaWiki using following commands:
   #Create a Helm Chart for MediaWiki
   helm create mediawiki

   #Modify Values in the created values.yaml file:
   values.yaml

# Default values for mediawiki.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

replicaCount: 1

image:
  repository: mediawiki
  pullPolicy: IfNotPresent
  # Overrides the image tag whose default is the chart appVersion.
  tag: "latest"

imagePullSecrets: []
nameOverride: ""
fullnameOverride: ""

serviceAccount:
  # Specifies whether a service account should be created
  create: true
  # Automatically mount a ServiceAccount's API credentials?
  automount: true
  # Annotations to add to the service account
  annotations: {}
  # The name of the service account to use.
  # If not set and create is true, a name is generated using the fullname template
  name: ""

podAnnotations: {}
podLabels: {}

podSecurityContext: {}
  # fsGroup: 2000

securityContext: {}
  # capabilities:
  #   drop:
  #   - ALL
  # readOnlyRootFilesystem: true
  # runAsNonRoot: true
  # runAsUser: 1000

service:
  type: ClusterIP
  port: 80

ingress:
  enabled: true
  className: ""
  annotations: {}
    # kubernetes.io/ingress.class: nginx
    # kubernetes.io/tls-acme: "true"
  hosts:
    - host: mediawiki.example.com
      paths:
        - path: /
          pathType: Prefix
  tls: []
  #  - secretName: chart-example-tls
  #    hosts:
  #      - chart-example.local

resources: {}
  # We usually recommend not to specify default resources and to leave this as a conscious
  # choice for the user. This also increases chances charts run on environments with little
  # resources, such as Minikube. If you do want to specify resources, uncomment the following
  # lines, adjust them as necessary, and remove the curly braces after 'resources:'.
  # limits:
  #   cpu: 100m
  #   memory: 128Mi
  # requests:
  #   cpu: 100m
  #   memory: 128Mi

livenessProbe:
  httpGet:
    path: /
    port: http
readinessProbe:
  httpGet:
    path: /
    port: http

autoscaling:
  enabled: false
  minReplicas: 1
  maxReplicas: 100
  targetCPUUtilizationPercentage: 80
  # targetMemoryUtilizationPercentage: 80

# Additional volumes on the output Deployment definition.
volumes: []
# - name: foo
#   secret:
#     secretName: mysecret
#     optional: false

# Additional volumeMounts on the output Deployment definition.
volumeMounts: []
# - name: foo
#   mountPath: "/etc/foo"
#   readOnly: true

nodeSelector: {}

tolerations: []

affinity: {}

#Install the Helm chart:
helm install mediawiki ./mediawiki

5. Monitor Deployment using following command:
   helm install mediawiki ./mediawiki

6.Access MediaWiki:
  http://mediawiki.example.com/

Attached screenshot for reference:
![image](https://github.com/Sakshi-19-99/mediawiki/assets/71216065/81528ced-8582-4f9b-bdb7-b1738c5584f7)



