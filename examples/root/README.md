# Consul Cluster Example

This folder shows an example of Terraform code that uses the [consul-cluster](/modules/consul-cluster) module to deploy 
a [Consul](https://www.consul.io/) cluster in [Google Cloud](https://cloud.google.com/). The cluster consists of two 
Compute Instance Groups: one with Consul server nodes, which are responsible for being part of the [consensus 
quorum](https://www.consul.io/docs/internals/consensus.html), and one with client nodes, which  would typically run 
alongside your apps:

![Consul architecture](/_docs/architecture.png)

You will need to create a [Custom Image](https://cloud.google.com/compute/docs/images) 
that has Consul installed, which you can do using the [consul-image example](/examples/consul-image)). Note that to keep 
this example simple, both the server Instance Group and client Instance Group are running the exact same Custom Image. 
In real-world usage, you'd probably have multiple client Instance Groups, and each of those Instance Groups would run a
different Custom Image that has the Consul agent installed alongside your apps.

For more info on how the Consul cluster works, check out the [consul-cluster](/modules/consul-cluster) documentation.



## Quick start

To deploy a Consul Cluster:

1. `git clone` this repo to your computer.
1. Build a Consul Custom Image. See the [consul-image example](/examples/consul-image) documentation for instructions. 
   Make sure to note down the ID of the Custom Image.
1. Install [Terraform](https://www.terraform.io/).
1. Open `vars.tf` and fill in any other variables that don't have a default, including putting your Custom Image ID into
   the `source_image` variable.
1. Run `terraform init`.
1. Run `terraform get`.
1. Run `terraform plan`.
1. If the plan looks good, run `terraform apply`.
1. Run the [consul-examples-helper.sh script](/examples/consul-examples-helper/consul-examples-helper.sh) to 
   print out the IP addresses of the Consul servers and some example commands you can run to interact with the cluster:
   `../consul-examples-helper/consul-examples-helper.sh`.

