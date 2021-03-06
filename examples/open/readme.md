An example that launches a redis cluster inside a VPC with open access.


```terraform

provider "aws" {
  region = "us-east-1"
}

module "elasticache_redis" {
  source = "github.com/turnerlabs/terraform-aws-elasticache-redis?ref=v1.1"

  cluster_id = "myteam-myapp-dev"

  vpc_id = "vpc-d070efb3"
  private_subnet_ids = "subnet-020d8b59,subnet-13f50b64"

  engine_version = "2.8.24"
  instance_type = "cache.m3.medium"
  maintenance_window = "sun:05:00-sun:06:00"

  tag_name = "redis"
  tag_environment = "dev"
  tag_team = "myteam"
  tag_application = "myapp"
}

resource "aws_security_group_rule" "access_in" {
  security_group_id = "${module.elasticache_redis.cache_security_group_id}"
  type        = "ingress"
  from_port   = 6379
  to_port     = 6379
  protocol    = "tcp"
  cidr_blocks = ["0.0.0.0/0"]
}

resource "aws_security_group_rule" "access_out" {
  security_group_id = "${module.elasticache_redis.cache_security_group_id}"
  type        = "egress"
  from_port   = 6379
  to_port     = 6379
  protocol    = "tcp"
  cidr_blocks = ["0.0.0.0/0"]
}

```
