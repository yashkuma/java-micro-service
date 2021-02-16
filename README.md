# java-micro-service
Java spring boot microservice CICD using AWS Codebuild, Code pipeline, ECS.


Create a CodeBuild build project.	
------------------------------------------

1.In the AWS CodeBuild console at https://console.aws.amazon.com/codesuite/codebuild/home, create a build project, and specify its name.

2.Select the source.	
This pattern uses Git/CodeCommit for the code repository, so choose Git or CodeCommit from the available options. 
Assuming Code has already been pushed to the Git or CodeCommit Respository.

3.Select a repository.	
Select the repository from which you want to build the code. Use the Repo pushed in above step.

4.Select the environment.	
You can select from a list of managed images or opt for a custom image using Docker. 
This pattern uses a managed image (Ubuntu).

5.Choose a service role.	
You can create a service role or select from a list of existing roles.

6.Create a buildspec file.	
buildspec.yml file is attached, update your ECR credentials, image name.

7.Opt for artifacts (optional).	
Configure the build project for artifacts, if required.

8.Configure Amazon CloudWatch logs.	
Configure the build project Amazon CloudWatch logs, if required. This step is optional but recommended. Charges are applicable.

9.Opt for Amazon S3 logs (optional).	
Configure the build project for Amazon Simple Storage Service (Amazon S3) logs, if you want to store the logs.

Notes: Codebuild will require permission to access Container Registry (ECR). Add AmazonEC2ContainerRegistryFullAccess policy to the Codebuild role created by aws.


=================================================================================================================

Configure the pipeline in AWS CodePipeline
------------------------------------------

1.Create a pipeline.	
In the AWS CodePipeline console at https://console.aws.amazon.com/codesuite/codepipeline/home, create a pipeline and specify its name.

2.Select a service role.	
Create a service role or select from the list of existing service roles.

3.Opt for an artifact store.	
If you want Amazon S3 to create a bucket and store the artifacts in it, use the default location. Or, select a custom location and specify an existing bucket.

4.Specify the source provider.	
Choose GitHub from the list of source providers.

5.Select the repository and branch of the code.	

6.Change detection options.	
The options are GitHub Webhooks and AWS CodePipeline. This pattern uses GitHub Webhooks.

7.Select a build provider.	
Select AWS CodeBuild as the build provider, then select the project name. You can choose Jenkins if your code was built using Jenkins.

8.Choose a deploy provider.	
Select Amazon ECS as the deploy provider from the list of available options. Create ECS Cluster/Task/Service, Use Container/Image details (ECR details) and Select the cluster name, the service name, the image definitions file, if any, and a deployment timeout value, if required. Choose "Create pipeline."

Note: In case of any S3 read permission issue, Codepipeline will require permission to access S3 bucket where artifacts are being stored. Add AmazonS3FullAccess policy to the codepipeline role created by AWS.
