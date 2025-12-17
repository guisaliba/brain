- open source tool developed by HashiCorp
- declarative language to manage resources
- three phases
	1. code
	2. plan
	3. apply
- code: a set of arguments that define the actual resources. say you want to build a VM, a K8s cluster and a VPC that houses the first two resources. they do not come out of thin air, they are coded as their own files e.g.: `vm.tf`, `k8s.tf`, `network.tf`.
- plan: Terraform doesn't know what your code is. once they are written, they are simply instructions, but Terraform doesn't see them as resources yet, it doesn't know that it has to create or change the `vm.tf`, `k8s.tf`and `network.tf`. plan is simply another CLI command that tells Terraform to plan the creation of these guys.
- apply: Terraform works against the cloud provider (e.g.: AWS) using **real** APIs (your API token for example) to **actually** spin up those resources. it outputs variables such as the Kubernetes cluster name, or the VM public/private IP.

- 