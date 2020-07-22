##AWS

###S3
- [AWS S3 Tutorial](https://www.youtube.com/watch?v=L3dYocCSU-E) - step-by-step walkthrough
###Lambda
- [What is Lambda?](https://www.youtube.com/watch?v=97q30JjEq9Y)
 - a compute service that lets you run code without provisioning or managing servers. [youtube 1:17](https://youtu.be/EpW28dvm_qo?t=77)
 
####Serverless
- No server to provision or manage
- Automatically scales with usage
- Never pay for idle
- Highly available
- e.g. Amazon DynamoDB, Amazon API Gateway, AWS Step Functions, Amazon Simple Queue Service

####Container
- standard unit of software that packages up code and all its dependencies
- configuration, code, dependencies, runtime engine, all packaged into an image which is called docker. Then instanciate the image into a container
- applications run quickly and reliably form one computing environment to another
- e.g. Kubernetes, Amazon EKS, Amazon ECS, Docker Swarm

####Environment
#####Serverless

| Syntax | Serverless | Container |
| ----------- | ----------- | ----------- |
| Infrastructure | managed by Cloud Provider, scale automatically, no patching headache | Users controlr underlying infrastructure - VM size, OS, AMI, require management and orchestration, master/node HA, VM failover, AMI rehydration |
| Software | cannot install  e.g. web server, app server, can installed code libraries | install any software, prepackaged images with different sofwares available |
| Configuration | selection of compute power, 128MB to 3GB memory, 1 sec to 15 mins time limit | adjust VM parameters |
| Hardware | No hard disk attached, limited package size can be deployed | hard disks attached to nodes |
| Superpower | easier to onboard, focus on solving business problem from get go | complete control of environment rich ecosystem |

####[User cases](https://youtu.be/EpW28dvm_qo?t=403)
- shine at event driven architecture, native integiration with... 