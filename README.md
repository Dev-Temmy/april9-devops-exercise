
# April9 DevOps Exercise

------

The purpose of this is to help you get familiar with April9's DevOps tools and the base infrastructure. We use TeamCity (CI Tool) to build our app, package into a container, and push to AWS ECR. Afterwards we use Octopus Deploy (CD Tool) to deploy the build container and infrastructure using AWS CloudFormation. 

Your task is to provision a small infrastructure through AWS CloudFormation that consists of a load balancer and an ecs cluster. Your load balancer will handle all client requests and forward it to a container hosted on an ecs cluster (See the infrastructure diagram below). You don't need to build your own custom docker image to host on aws. Instead use the docker image https://hub.docker.com/r/nginxdemos/hello/. Note: You are not expected to get the docker image running properly in the aws environment!

How to approach the problem:

1. Clone/Fork this repository into your Github account
1. Create a CloudFormation file in yaml and insert your resource blocks:
   1. `AWS::ElasticLoadBalancingV2::ListenerRule`
   2. `AWS::ElasticLoadBalancingV2::TargetGroup`
   3. `AWS::ECS::TaskDefinition`  (Use Fargate Compatibilities, NetworkMode - `awsvpc`)
      - Container Image: `nginxdemos/hello`
   4. `AWS::ECS::Service`
   5. `AWS::EC2::SecurityGroup`
      - One security group for your load balancer (use port 80)
      - One security group for your ecs cluster (reference the security group of the load balancer for ingress)
2. Deploy your CloudFormation file! If it deploys successfully you're done!
3. Commit and push your changes to the repo
3. Share the repo with us