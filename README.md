Ingress Endpoint Helm Chart

This Helm Chart deploys a simple Ingress endpoint for existing Kubernetes Services. It does not include application Pods or Services—only the Ingress resource for routing external traffic.

🚀 Overview

This chart is ideal when you want to quickly create an Ingress resource to expose existing backend services to external traffic in a Kubernetes environment.

Use cases include:

Adding Ingress rules to already deployed applications.

Configuring Ingress for Services deployed via other Helm charts or manually.

Managing simple routing for specific hostnames or paths.


✨ Features

Ingress Resource Only: No Deployment or Service is deployed.

Flexible Configuration: Customize hostname, path, backend service, and TLS using values.yaml.

Versatile: Works with any existing Service without application dependency.


📚 Prerequisites

Kubernetes cluster (v1.19+ recommended)

Helm (v3.0+)

An installed Ingress Controller (e.g., NGINX, Traefik, AWS ALB, etc.)


📦 Installation (via GitHub Pages)

This chart is hosted via GitHub Pages. You can install it directly using the following commands:

helm repo add ingress-endpoint https://devnekoops.github.io/ingress-endpoint/
helm repo update
helm install my-ingress ingress-endpoint/ingress-endpoint -n ingress-system --create-namespace \
  --set ingress.hosts[0]="example.co.jp" \
  --set ingress.serviceName="awesome-service" \
  --set ingress.servicePort=8080

🔧 Example values.yaml

ingress:
  enabled: true
  ingressClassName: "nginx"
  path: "/"
  pathType: Prefix
  serviceName: "awesome-service"
  servicePort: 8080
  annotations: {}
  hosts:
    - "example.co.jp"
  tls:
    - secretName: "example-secret"
      hosts:
        - example.co.jp

🛠️ Uninstallation

helm uninstall my-ingress -n ingress-system

⚙️ Configuration Options

Parameter	Description	Default

ingress.enabled	Whether to enable the Ingress resource	true
ingress.ingressClassName	Name of the IngressClass to use	nginx
ingress.hosts	List of hostnames to expose via Ingress	[]
ingress.path	Path to route	"/"
ingress.pathType	Type of path matching (Prefix, Exact, etc.)	Prefix
ingress.serviceName	Target Kubernetes Service name	""
ingress.servicePort	Target Service port number	80
ingress.annotations	Custom annotations for the Ingress resource	{}
ingress.tls	TLS settings (list of secretName + hosts)	[]


🤝 Contributing

We welcome contributions of all kinds—bug reports, feature requests, documentation improvements, and code.

📄 License

Apache 2.0 License

