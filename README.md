## Terraform module for GKE with custom buckets

To be able to use following terraform module please follow the documentation. 


## Requirements

* Terraform >= 0.11.14
* provider.google: version = "~> 2.20"



## Calling module

Your `main.tf` should look like this
```
module "gke_cluster" {
    source  = "../../"
    cluster_name = "practice-cluster"  # name of your cluster
    google_region = "us-central1-c"  # region you wanna deploy to
    google_project_id =  "concrete-potion-329118"  #your project id
    cluster_node_count = "2" 
    cluster_version = "1.19"
    google_credentials = "./service_account.json" # service account
    image_type        = "COS"
    disk_size_in_gb   = "10"
    machine_type      = "n1-standard-2"
    auto_repair     = true
    auto_upgrade    = false
    gce_ssh_user    = "default-user"
    labels            = {
        "label" = "practice-project"
    }
}

```

After you finish with defining all required variables go ahead and run `terraform init`

```
terraform init
```

After terraform finish with initialization go ahead and apply 

## Variables

For more info, please see the [variables file](?tab=inputs).

| Variable               | Description                         | Default                                               | Type |
| :--------------------- | :---------------------------------- | :---------------------------------------------------: | :--------------------: |
| `google_project_id` | Google account project id | `(Required)` | `string` |
| `google_region` | Name of the namespace | `(Required)` | `string` |
| `cluster_version` | Version of the cluster. | `(Required)` | `string` |
| `cluster_node_count` | Number of nodes for the cluster. | `(Required)` | `string` |
| `google_credentials` | your google service account `example.json`| `(Required)` | `string` |
| `cluster_network` |The name or self_link of the Google Compute Engine network to which the cluster is connected. | `(Optional)` | `string` |
| `cluster_name` | The name of the cluster, unique within the project and location. | `(Required)` | `string` |
| `machine_type` | The name of a Google Compute Engine machine type. | `(Optional)` | `string` |
| image_type     | The disk side of each node in the cluster         |  `(Optional)`| `string`  |  
| labels         | The label of the node in the cluster.             |  `(optional) | `map`| 
| `auto_upgrade`  |  The autoupgrade of the node in the cluster.     |  `(optional)` |  `string`  |                                         |              |
| `auto_repair`   |  The autorepair of the node in the cluster.      |  `(optional)` |  `string`  |  
| `preemptible_nodes`   |  The preemptible  of the node in the cluster. |  `(optional)` |  `string`  | 
| `node_pool`   |  The name of the node_pool in the cluster.            |  `(optional)` |  `string`  |  
| `gce_ssh_user`   |  The name of the node_pool in the cluster.            |  `(optional)` |  `string`  |  
| `gce_ssh_pub_key_file`   |  The name of the node_pool in the cluster.            |  `(optional)` |  `string`  |  

## Output

Use the following output to learn how to ssh to your nodes:
```
output "ssh_info"
```



