<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# Build a Kubernetes Controller

**Project Link:** [View Project](https://nextwork.ai/projects/b5c583b1-6aa9-45ca-876b-d155a6a7b2b6)

**Author:** Dennis Chigozirim

---

![Build a Kubernetes Controller](https://nextwork.ai/vibrant_orange_loyal_hoiho/uploads/b5c583b1-6aa9-45ca-876b-d155a6a7b2b6_xj3rxmd8)

## Project Vision: Reconciliation Loops in Kubernetes

### Why reconciliation loops matter for reliable systems

In this project, I'm building a custom Kubernetes controller so that I can demonstrate how it works, I declare a desired state ("I want 3 echo server pods") and a reconciliation loop continuously creates, fixes, and scales pods to match.

## Proving Self-Healing: The Controller in Action

![Proving Self-Healing: The Controller in Action](https://nextwork.ai/vibrant_orange_loyal_hoiho/uploads/b5c583b1-6aa9-45ca-876b-d155a6a7b2b6_uii89y6o)

### Testing the control loop under perturbation

In this step, I'm testing the controller's ability to self-heal and enforce desired state, so that I can prove the reconciliation loop correctly resolves drift and updates the cluster when the specification changes.

### Controller response to manual drift

When I ran kubectl scale to set replicas to 1, the controller detected the drift and corrected the Deployment back to 3 replicas.

## Implementing the Reconciliation Loop

### Building the observe-compare-act cycle

In this step, I'm implementing the full Reconcile function with observe, compare, and act phases. I'll add RBAC permissions and run the controller to see pods appear, then I'll close the feedback loop so that the Deployment changes trigger re-reconciliation.

![Implementing the Reconciliation Loop](https://nextwork.ai/vibrant_orange_loyal_hoiho/uploads/b5c583b1-6aa9-45ca-876b-d155a6a7b2b6_okgskyeh)

### The three phases of reconciliation explained

The three phases are: first I fetch the EchoServer resource, then I check if the actual state matches the desired state, finally I create, update, or delete resources to reconcile the difference.

## Setting Up the Local Cluster and Toolchain

### Preparing the Kubernetes environment

In this step, I'm setting up a local kubernetes cluster so that I can begin my project, to build a custom Kubernetes controller, I need a local cluster to run it against and the Kubebuilder SDK to scaffold the project.

Without a running cluster, there is nothing to reconcile. In this step, I will install three tools and spin up a local Kubernetes cluster using kind (Kubernetes in Docker). The three tools are kind, kubectl and kubebuilder.

### Installing kind, kubectl, and Kubebuilder

I installed kind, kubectl and kubebuilder, and kind get clusters returns "kind".

## Scaffolding the Operator and Defining the API

### Generating the CRD and project structure

In this step, I'll scaffold the project with Kubebuilder and define the EchoServer API types. Then I'll install the CRD, apply a sample resource, and observe the empty controller.

![Scaffolding the Operator and Defining the API](https://nextwork.ai/vibrant_orange_loyal_hoiho/uploads/b5c583b1-6aa9-45ca-876b-d155a6a7b2b6_im29iw1t)

### The open-loop gap: desired state without an actuator

The Deployment was not created because this is the designed gap. The desired state is declared but no actuator exists to create the Deployment. The Reconcile function body is empty.

## Secret Mission: Closing the Feedback Loop with Status Conditions

### Reporting observed state back to the API server

In this project extension, I see the Available condition with status "True" and reason AllReplicasAvailable, which tells me that the controller successfully reconciled the desired state of 5 replicas and all pods are currently up and running.

## Reflections and Key Takeaways

### Tools and concepts mastered

The key tools I used include Kubebuilder to scaffold the operator, Go for writing the controller logic, and Kind (Kubernetes in Docker) to run a local cluster. Key concepts I learned include how the Kubernetes reconciliation loop works, how to define Custom Resource Definitions (CRDs), and how controllers actively enforce desired state (self-healing).

### Time and challenges

This project took me approximately a few hours to complete. The most challenging part was debugging the initial setup, specifically resolving the Go version mismatch and fixing the SchemeBuilder registration errors in the API types.

I did this project today to learn how to build custom Kubernetes operators using the Operator pattern. Another skill I want to learn is writing more advanced admission webhooks, or learning how to package and deploy operators using Helm or OLM (Operator Lifecycle Manager).
