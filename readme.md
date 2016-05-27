# terraform-aws-elasticache-redis

A Terraform module that represents an AWS ElastiCache Redis cluster.  Note that a default security group is created and outputted that can be extended.  See basic example usage below and more examples [here](/examples).

### Usage

```terraform
module "elasticache_redis" {
  source = "github.com/turnerlabs/terraform-aws-elasticache-redis"

  vpc_id = "vpc-20f74844"
  private_subnet_ids = "subnet-4a887f3c,subnet-76dae35d"

  engine_version = "2.8.24"
  instance_type = "cache.m3.medium"
  maintenance_window = "sun:05:00-sun:06:00"

  tag_name = "redis"
  tag_billing = "90193400"
  tag_environment = "dev"
  tag_creator = "me@email.com"
  tag_customer = "cnn"
  tag_team = "myteam"
  tag_product = "my-app"
}
```

### Variables

- `vpc_id` - ID of VPC meant to house the cache
- `private_subnet_ids` - Comma delimited list of private subnet IDs
- `engine_version` - Cache engine version (default: `2.8.24`)
- `instance_type` - Instance type for cache instance (default: `cache.m3.medium`)
- `maintenance_window` - 60 minute time window to reserve for maintenance
  (default: `sun:05:00-sun:06:00`)
- `tag_name`
- `tag_description`
- `tag_creator`
- `tag_product`
- `tag_customer`
- `tag_owner`
- `tag_environment`
- `tag_costcenter`

### Outputs

- `cache_security_group_id` - Security group ID of the cache cluster
- `hostname` - Public DNS name of cache node
- `port` - Port of cache instance
- `endpoint` - Public DNS name and port separated by a `:`
