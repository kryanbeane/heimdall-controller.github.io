---
layout: home
---

# Welcome to the Heimdall Wiki!
Heimdall is an open-source tool created for a final year project to implement Atomic Resource Ownership in multi-operator Kubernetes environments. Heimdall resolves conflicting Resource states between Operators by allowing the configuration of an Owner. This owner is solely allowed to change that Resource, preventing diverging states and conflicting configurations.

## The Problem
In Kubernetes, Operators and Controllers are responsible for reconciling the actual state of a resource with its desired state. However, when two Operators with conflicting desired states are both reconciling the same resource, it leads to an ongoing state change, causing confusion and issues. Heimdall solves this problem by providing a way to monitor resources and prevent unauthorized changes.
