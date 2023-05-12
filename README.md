# k8s-webhooks
What is webhook in k8s and how it works


- In Kubernetes, webhooks are mechanisms used to extend and customize the behavior of the API server. They allow you to intercept and modify requests and responses flowing in and out of the API server. There are primarily two types of webhooks in Kubernetes: admission webhooks and conversion webhooks.

# Admission Webhooks:

- Admission webhooks allow you to intercept and modify requests before they are persisted to the cluster or before they reach the target resource.

## There are two types of admission webhooks:
* ValidatingWebhook: It performs validation on incoming requests and either allows or denies the request based on defined policies.
* MutatingWebhook: It intercepts requests and modifies them before they are persisted or sent to the target resource.

Example: Imagine a scenario where you want to enforce a custom policy that requires all Pods in a namespace to have specific labels. You can create a ValidatingWebhook that intercepts the Pod creation requests and checks for the presence of the required labels. If the labels are not present, the webhook can deny the request.

# Conversion Webhooks:

- Conversion webhooks are used for converting resources between different versions and modifying the behavior of resources during the conversion process.
- They allow you to customize the behavior of the API server during serialization and deserialization of resources.

Example: Let's say you want to introduce a new custom resource definition (CRD) to your cluster. However, you want to ensure backward compatibility by automatically converting the old resource instances to the new format. You can create a ConversionWebhook that intercepts requests for the old resource type and performs the necessary conversion to the new format.

# To use webhooks in Kubernetes, you need to follow these general steps:

## Implement the webhook logic: 
  - You need to write the webhook logic in your preferred programming language. This typically involves creating an HTTP server that handles the incoming requests, performs the necessary operations, and returns the response.
## Create a webhook configuration: 
  - You need to define a Kubernetes webhook configuration object that specifies details like the URL of your webhook server, the type of webhook (ValidatingWebhook or MutatingWebhook), and other configuration parameters.
## Deploy the webhook: 
  - Deploy your webhook server and the webhook configuration to your Kubernetes cluster. The webhook server needs to be accessible to the Kubernetes API server
## Register the webhook configuration: 
  - Register the webhook configuration with the Kubernetes API server using the ValidatingWebhookConfiguration or MutatingWebhookConfiguration resource.
- Once the webhook is registered and running, Kubernetes will send requests to your webhook server based on the defined configuration, and your server can perform the necessary operations and return the response to the API server.

- It's important to note that configuring and managing webhooks requires a good understanding of Kubernetes API server, authentication, and networking concepts. Detailed implementation steps and code examples for webhooks are beyond the scope of a text-based conversation. It's recommended to refer to the Kubernetes documentation and relevant resources for comprehensive guides and examples on implementing webhooks in Kubernetes.
