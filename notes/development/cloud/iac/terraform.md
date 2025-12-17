- open source tool developed by HashiCorp
- declarative language to manage resources
- three phases
	1. code
	2. plan
	3. apply

- code: a set of arguments that define the actual resources. say you want to build a VM, a K8s cluster and a VPC that houses the first two resources. they do not come out of thin air, they are coded as their own files e.g.: `vm.tf`, `k8s.tf`, `network.tf`
- plan: Terraform doesn't know what your code is. once they are written, they are simply instructions, but Terraform doesn't see them as resources yet, it doesn't know that it has to create or change the `vm.tf`, `k8s.tf`and `network.tf`. plan is simply another CLI command that tells Terraform to plan the creation of these guys.
- apply: Terraform works against the cloud provider (e.g.: AWS) using **real** APIs (your API token for example) to **actually** spin up those resources. it outputs variables such as the Kubernetes cluster name, or the VM public/private IP

- the combination of the three phases defines a so called **provider**
- a provider allows you to connect you to an actual cloud provider (AWS, Azure, etc.): that's IaaS -> these cloud providers will host/support the infrastructure you're building (e.g.: the VM, Cluster and VPC of the latest example)
- you can use a Terraform provider to spin up platforms that serve as cloud foundry: that's PaaS -> platforms that serve as a service for cloud resources building
- even software related stuff such as Cloudflare can be used through a Terraform provider: that's SaaS

- Terraform powers best DevOps practices: it is a DevOps first tool
- adding a new resource on top of the existing Terraform environment isn't a "hard reset". Terraform looks to the current "world" and is capable to understand what you're adding and what has been there already
- on the previous example, adding a Load Balancer in front of the VM, K8s and VPC would also require it to go through the Terraform pipeline again: code, plan, apply
- once Terraform plan kicks in, it realizes that only the Load Balancer is a new folk on the town. plan will not recreate the other three. this avoids configuration drifts and potential issues