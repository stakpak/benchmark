# Convert Terraform code to Eraser Diagram Benchmark

## Example 1: Terraform EKS Module

### Source

<https://github.com/terraform-aws-modules/terraform-aws-eks>

### Stakpak

#### Diagram

![Result Diagram](./assets/example1-stakpak.png)

#### Code

```
direction right

aws_cloud {
  aws_eks [icon: "aws-eks", label: "Elastic Kubernetes Service"] {
    aws_eks_cluster.this [icon: "aws-eks", label: "EKS Cluster"]
    aws_eks_access_entry.this [icon: "aws-eks", label: "EKS Access Entry"]
    aws_eks_access_policy_association.this [icon: "aws-eks", label: "EKS Access Policy Association"]
    aws_eks_addon.this [icon: "aws-eks", label: "EKS Addon"]
    aws_eks_addon.before_compute [icon: "aws-eks", label: "EKS Addon Before Compute"]
    aws_eks_identity_provider_config.this [icon: "aws-eks", label: "EKS Identity Provider Config"]
  }
  aws_ec2 [icon: "aws-ec2", label: "EC2"] {
    aws_ec2_tag.cluster_primary_security_group [icon: "aws-ec2", label: "EC2 Tag"]
    aws_security_group.cluster [icon: "aws-ec2", label: "Security Group"]
    aws_security_group_rule.cluster [icon: "aws-ec2", label: "Security Group Rule"]
    aws_security_group.node [icon: "aws-ec2", label: "Security Group"]
    aws_security_group_rule.node [icon: "aws-ec2", label: "Security Group Rule"]
  }
  aws_cloudwatch [icon: "aws-cloudwatch", label: "CloudWatch"] {
    aws_cloudwatch_log_group.this [icon: "aws-cloudwatch", label: "CloudWatch Log Group"]
  }
  aws_iam [icon: "aws-iam", label: "IAM"] {
    aws_iam_openid_connect_provider.oidc_provider [icon: "aws-iam", label: "IAM OpenID Connect Provider"]
    aws_iam_policy_document.assume_role_policy [icon: "aws-iam", label: "IAM Policy Document"]
    aws_iam_policy_document.cni_ipv6_policy [icon: "aws-iam", label: "IAM Policy Document"]
    aws_iam_policy.cni_ipv6_policy [icon: "aws-iam", label: "IAM Policy"]
    aws_iam_policy.cluster_encryption [icon: "aws-iam", label: "IAM Policy"]
    aws_iam_role.this [icon: "aws-iam", label: "IAM Role"]
    aws_iam_role_policy_attachment.this [icon: "aws-iam", label: "IAM Role Policy Attachment"]
    aws_iam_role_policy_attachment.additional [icon: "aws-iam", label: "IAM Role Policy Attachment"]
    aws_iam_role_policy_attachment.cluster_encryption [icon: "aws-iam", label: "IAM Role Policy Attachment"]
  }
  aws_kms [icon: "aws-kms", label: "KMS"] {
    module.kms [icon: "aws-kms", label: "KMS Module"]
  }
  tls [icon: "tls", label: "TLS"] {
    data.tls_certificate.this [icon: "tls", label: "TLS Certificate"]
  }
  time [icon: "time", label: "Time"] {
    resource.time_sleep.this [icon: "time", label: "Time Sleep"]
  }
  eks_managed_node_group [icon: "eks", label: "EKS Managed Node Group"] {
    module.eks_managed_node_group [icon: "eks", label: "EKS Managed Node Group Module"]
  }
  self_managed_node_group [icon: "eks", label: "Self Managed Node Group"] {
    module.self_managed_node_group [icon: "eks", label: "Self Managed Node Group Module"]
  }
  fargate_profile [icon: "fargate", label: "Fargate Profile"] {
    module.fargate_profile [icon: "fargate", label: "Fargate Profile Module"]
  }
}

// Connections
data.aws_caller_identity.current > data.aws_iam_session_context.current
module.kms > aws_eks_cluster.this
aws_iam_role_policy_attachment.this > aws_eks_cluster.this
aws_security_group_rule.cluster > aws_eks_cluster.this
aws_security_group_rule.node > aws_eks_cluster.this
aws_cloudwatch_log_group.this > aws_eks_cluster.this
aws_iam_policy.cni_ipv6_policy > aws_eks_cluster.this
aws_eks_cluster.this > aws_ec2_tag.cluster_primary_security_group
aws_eks_cluster.this > aws_eks_access_entry.this
aws_eks_cluster.this > aws_eks_access_policy_association.this
aws_eks_access_entry.this > aws_eks_access_policy_association.this
data.aws_iam_session_context.current > module.kms
aws_security_group.cluster > aws_security_group_rule.cluster
aws_eks_cluster.this > data.tls_certificate.this
aws_eks_cluster.this > aws_iam_openid_connect_provider.oidc_provider
data.aws_iam_policy_document.assume_role_policy > aws_iam_role.this
aws_iam_role.this > aws_iam_role_policy_attachment.this
aws_iam_role.this > aws_iam_role_policy_attachment.additional
aws_iam_policy.cluster_encryption > aws_iam_role_policy_attachment.cluster_encryption
aws_iam_role.this > aws_iam_role_policy_attachment.cluster_encryption
module.kms > aws_iam_policy.cluster_encryption
aws_eks_cluster.this > data.aws_eks_addon_version.this
aws_eks_cluster.this > aws_eks_addon.this
data.aws_eks_addon_version.this > aws_eks_addon.this
module.fargate_profile > aws_eks_addon.this
module.eks_managed_node_group > aws_eks_addon.this
module.self_managed_node_group > aws_eks_addon.this
aws_eks_cluster.this > aws_eks_addon.before_compute
data.aws_eks_addon_version.this > aws_eks_addon.before_compute
aws_eks_cluster.this > aws_eks_identity_provider_config.this
aws_eks_cluster.this > resource.time_sleep.this
aws_eks_cluster.this > resource.time_sleep.this
aws_eks_cluster.this > resource.time_sleep.this
aws_eks_cluster.this > resource.time_sleep.this
data.aws_iam_policy_document.cni_ipv6_policy > aws_iam_policy.cni_ipv6_policy
aws_security_group.node > aws_security_group_rule.node
resource.time_sleep.this > module.fargate_profile
resource.time_sleep.this > module.eks_managed_node_group
resource.time_sleep.this > module.eks_managed_node_group
resource.time_sleep.this > module.eks_managed_node_group
resource.time_sleep.this > module.eks_managed_node_group
resource.time_sleep.this > module.eks_managed_node_group
aws_eks_cluster.this > module.eks_managed_node_group
resource.time_sleep.this > module.self_managed_node_group
resource.time_sleep.this > module.self_managed_node_group
resource.time_sleep.this > module.self_managed_node_group
resource.time_sleep.this > module.self_managed_node_group
resource.time_sleep.this > module.self_managed_node_group
aws_eks_cluster.this > module.self_managed_node_group
```

### Metrics

- **LLM Time**: 21.462 Seconds
- **Total Time**: 25.281 Seconds
- **Total Cost**: $0.001678


### OpenAI o1-preview

#### Diagram

![Result Diagram](./assets/example1-o1.png)

#### Code
```
direction right

aws_cloud {
  aws_eks [icon: "aws-eks", label: "Elastic Kubernetes Service"] {
    aws_eks_cluster.this [icon: "aws-eks", label: "EKS Cluster"]
    aws_eks_access_entry.this [icon: "aws-eks", label: "EKS Access Entry"]
    aws_eks_access_policy_association.this [icon: "aws-eks", label: "EKS Access Policy Association"]
    aws_eks_addon.this [icon: "aws-eks", label: "EKS Add-ons"]
    aws_eks_addon.before_compute [icon: "aws-eks", label: "EKS Pre-Compute Add-ons"]
    aws_eks_identity_provider_config.this [icon: "aws-eks", label: "EKS Identity Provider Config"]
    module.fargate_profile [icon: "aws-eks", label: "EKS Fargate Profiles"]
    module.eks_managed_node_group [icon: "aws-eks", label: "EKS Managed Node Groups"]
    module.self_managed_node_group [icon: "aws-eks", label: "EKS Self-Managed Node Groups"]
  }

  aws_iam [icon: "aws-iam", label: "Identity and Access Management"] {
    aws_iam_role.this [icon: "aws-iam", label: "EKS Cluster IAM Role"]
    aws_iam_role_policy_attachment.this [icon: "aws-iam", label: "IAM Role Policy Attachment"]
    aws_iam_role_policy_attachment.additional [icon: "aws-iam", label: "Additional IAM Role Policy Attachment"]
    aws_iam_role_policy_attachment.cluster_encryption [icon: "aws-iam", label: "Cluster Encryption IAM Policy Attachment"]
    aws_iam_policy.cluster_encryption [icon: "aws-iam", label: "Cluster Encryption IAM Policy"]
    aws_iam_policy.cni_ipv6_policy [icon: "aws-iam", label: "CNI IPv6 IAM Policy"]
    aws_iam_openid_connect_provider.oidc_provider [icon: "aws-iam", label: "OIDC Provider"]
  }

  aws_kms [icon: "aws-kms", label: "Key Management Service"] {
    module.kms [icon: "aws-kms", label: "EKS KMS Key Module"]
  }

  aws_cloudwatch [icon: "aws-cloudwatch", label: "CloudWatch"] {
    aws_cloudwatch_log_group.this [icon: "aws-cloudwatch", label: "CloudWatch Log Group"]
  }

  aws_ec2 [icon: "aws-ec2", label: "Elastic Compute Cloud"] {
    aws_security_group.cluster [icon: "aws-ec2", label: "Cluster Security Group"]
    aws_security_group_rule.cluster [icon: "aws-ec2", label: "Cluster Security Group Rules"]
    aws_security_group.node [icon: "aws-ec2", label: "Node Security Group"]
    aws_security_group_rule.node [icon: "aws-ec2", label: "Node Security Group Rules"]
    aws_ec2_tag.cluster_primary_security_group [icon: "aws-ec2", label: "Cluster Primary Security Group Tag"]
  }
}

// Connections
aws_eks_cluster.this > aws_iam_role.this
aws_eks_cluster.this > aws_iam_openid_connect_provider.oidc_provider
aws_eks_cluster.this > aws_security_group.cluster
aws_eks_cluster.this > aws_security_group.node
aws_eks_cluster.this > aws_cloudwatch_log_group.this
aws_eks_cluster.this > module.kms
aws_iam_role_policy_attachment.this > aws_iam_role.this
aws_iam_role_policy_attachment.additional > aws_iam_role.this
aws_iam_role_policy_attachment.cluster_encryption > aws_iam_role.this
aws_iam_role.this > aws_iam_policy.cluster_encryption
aws_security_group_rule.cluster > aws_security_group.cluster
aws_security_group_rule.node > aws_security_group.node
aws_ec2_tag.cluster_primary_security_group > aws_security_group.cluster
aws_eks_access_entry.this > aws_eks_cluster.this
aws_eks_access_policy_association.this > aws_eks_access_entry.this
module.eks_managed_node_group > aws_eks_cluster.this
module.self_managed_node_group > aws_eks_cluster.this
module.fargate_profile > aws_eks_cluster.this
```

### Metrics

- **Total Time**: 67.541 Seconds
- **Total Cost**: $0.5904


## Example 2: Terraform EKS Module

### Source

<https://github.com/milliHQ/terraform-aws-next-js>

### Stakpak

#### Diagram

![Result Diagram](./assets/example2-stakpak.png)

#### Code
```
direction right

aws_cloud {
  aws_dynamodb [icon: "aws-dynamodb", label: "DynamoDB"] {
    aws_dynamodb_table.aliases [icon: "aws-dynamodb", label: "Aliases Table"]
    aws_dynamodb_table.deployments [icon: "aws-dynamodb", label: "Deployments Table"]
  }
  aws_iam [icon: "aws-iam", label: "Identity and Access Management"] {
    aws_iam_policy.cloudformation_permission [icon: "aws-iam", label: "CloudFormation Permission Policy"]
    aws_iam_role.cloudformation_permission [icon: "aws-iam", label: "CloudFormation Permission Role"]
    data_aws_iam_policy_document.cloudformation_permission [icon: "aws-iam", label: "CloudFormation Permission Document"]
    data_aws_iam_policy_document.cloudformation_permission_assume_role [icon: "aws-iam", label: "CloudFormation Permission Assume Role Document"]
    data_aws_iam_policy_document.access_static_deployment [icon: "aws-iam", label: "Access Static Deployment Document"]
  }
  aws_cloudfront [icon: "aws-cloudfront", label: "CloudFront"] {
    aws_cloudfront_cache_policy.this [icon: "aws-cloudfront", label: "Cache Policy"]
    data_aws_cloudfront_origin_request_policy.managed_all_viewer [icon: "aws-cloudfront", label: "Origin Request Policy"]
  }
  aws_region [icon: "aws-region", label: "Region"] {
    data_aws_region.current [icon: "aws-region", label: "Current Region"]
  }
  modules [icon: "aws-modules", label: "Modules"] {
    module.deploy_controller [icon: "aws-modules", label: "Deploy Controller"]
    module.statics_deploy [icon: "aws-modules", label: "Statics Deploy"]
    module.api [icon: "aws-modules", label: "API"]
    module.next_image [icon: "aws-modules", label: "Next Image"]
    module.proxy_config [icon: "aws-modules", label: "Proxy Config"]
    module.proxy [icon: "aws-modules", label: "Proxy"]
    module.cloudfront_main [icon: "aws-modules", label: "CloudFront Main"]
  }
}

// Connections
module.deploy_controller > data_aws_iam_policy_document.cloudformation_permission
module.statics_deploy > data_aws_iam_policy_document.cloudformation_permission
data_aws_iam_policy_document.cloudformation_permission > aws_iam_policy.cloudformation_permission
data_aws_iam_policy_document.cloudformation_permission_assume_role > aws_iam_role.cloudformation_permission
aws_iam_policy.cloudformation_permission > aws_iam_role.cloudformation_permission
data_aws_region.current > module.deploy_controller
aws_dynamodb_table.aliases > module.deploy_controller
aws_dynamodb_table.deployments > module.deploy_controller
module.cloudfront_main > module.statics_deploy
module.deploy_controller > module.statics_deploy
data_aws_region.current > module.statics_deploy
aws_dynamodb_table.aliases > module.statics_deploy
aws_dynamodb_table.deployments > module.statics_deploy
aws_iam_role.cloudformation_permission > module.statics_deploy
data_aws_region.current > module.api
aws_dynamodb_table.aliases > module.api
aws_dynamodb_table.deployments > module.api
module.statics_deploy > module.api
module.statics_deploy > data_aws_iam_policy_document.access_static_deployment
data_aws_iam_policy_document.access_static_deployment > module.next_image
data_aws_region.current > module.proxy_config
aws_dynamodb_table.aliases > module.proxy_config
module.statics_deploy > module.proxy_config
```

### Metrics

- **LLM Time**: 10.54 Seconds
- **Total Time**: 11.146 Seconds
- **Total Cost**: $0.001023


### OpenAI o1-preview

#### Diagram

![Result Diagram](./assets/example2-o1.png)

#### Code
```
direction right

aws_cloud {
  aws_dynamodb [icon: "aws-dynamodb", label: "Amazon DynamoDB"] {
    aws_dynamodb_table.aliases [icon: "aws-dynamodb-table", label: "DynamoDB Table - Aliases"]
    aws_dynamodb_table.deployments [icon: "aws-dynamodb-table", label: "DynamoDB Table - Deployments"]
  }

  aws_iam [icon: "aws-iam", label: "AWS Identity and Access Management"] {
    aws_iam_policy.cloudformation_permission [icon: "aws-iam-policy", label: "IAM Policy - CloudFormation Permission"]
    aws_iam_role.cloudformation_permission [icon: "aws-iam-role", label: "IAM Role - CloudFormation Permission"]
  }

  aws_lambda [icon: "aws-lambda", label: "AWS Lambda"] {
    module.deploy_controller [icon: "aws-lambda", label: "Lambda Function - Deploy Controller"]
    module.statics_deploy [icon: "aws-lambda", label: "Lambda Function - Statics Deploy"]
    module.api [icon: "aws-lambda", label: "Lambda Function - API"]
    module.next_image [icon: "aws-lambda", label: "Lambda Function - Next/Image"]
    module.proxy [icon: "aws-lambda", label: "Lambda Function - Proxy (Lambda@Edge)"]
  }

  aws_s3 [icon: "aws-s3", label: "Amazon S3"] {
    module.statics_deploy.static_bucket [icon: "aws-s3", label: "S3 Bucket - Static Content"]
  }

  aws_cloudfront [icon: "aws-cloudfront", label: "Amazon CloudFront"] {
    aws_cloudfront_cache_policy.this [icon: "aws-cloudfront", label: "CloudFront Cache Policy"]
    module.cloudfront_main [icon: "aws-cloudfront", label: "CloudFront Distribution"]
  }
}

// Connections
aws_iam_policy.cloudformation_permission > aws_iam_role.cloudformation_permission
aws_iam_role.cloudformation_permission > module.statics_deploy
aws_dynamodb_table.aliases > module.deploy_controller
aws_dynamodb_table.deployments > module.deploy_controller
aws_dynamodb_table.aliases > module.statics_deploy
aws_dynamodb_table.deployments > module.statics_deploy
module.deploy_controller > module.statics_deploy
module.statics_deploy > module.api
module.statics_deploy > module.next_image
module.statics_deploy > module.cloudfront_main
module.next_image > module.cloudfront_main
module.proxy_config > module.cloudfront_main
module.proxy > module.cloudfront_main
```

### Metrics

- **Total Time**: 61.910 Seconds
- **Total Cost**: $0.45