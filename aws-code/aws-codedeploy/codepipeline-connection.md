# CodePipeline Connection

In an automated AWS CodePipeline, the code to be deployed by CodeDeploy is passed as a deployment artifact from the build stage. CodeDeploy then uses this artifact, along with an `AppSpec` file, to determine what code to install and where to install it on the target EC2 instances. 1. The CodeBuild processIn a typical CodePipeline setup, the build stage uses AWS CodeBuild. During this stage, CodeBuild performs several key tasks:

* It compiles the application's source code, runs tests, and packages the application and its dependencies into a single deployment bundle.
* Crucially, this bundle must also contain a YAML-formatted file named `appspec.yml` at its root.
* The `appspec.yml` file contains instructions for CodeDeploy about the deployment. It specifies which files to copy and where to put them on the target instances.&#x20;
*

2\. The AppSpec fileThe `appSpec.yml` file is the key to telling CodeDeploy what to do with the code it receives. A typical `appspec.yml` file for an EC2 deployment includes sections for:&#x20;

* `files`: This section maps the source files inside the deployment bundle to their destination directories on the EC2 instances.
* `hooks`: This section defines scripts to be run during different phases of the deployment lifecycle. For example, a `BeforeInstall` hook might be used to run a script that stops the web server, while an `ApplicationStart` hook would run a script to start the application after the new code is in place.&#x20;
*

3\. The CodePipeline-to-CodeDeploy flowThe process of passing the code artifact from CodeBuild to CodeDeploy unfolds as follows:

1. CodeBuild output: The CodeBuild project's `buildspec.yml` file specifies the deployment bundle (for example, a ZIP file containing the compiled RPM package and the `appspec.yml` file) as an output artifact. CodeBuild automatically places this artifact in a designated S3 bucket.
2. CodePipeline artifact store: CodePipeline uses an S3 bucket as a central artifact store for the entire pipeline. The build stage places its output artifact into this S3 bucket.
3. CodeDeploy action: The deploy stage of the pipeline is configured with a CodeDeploy action. This action is set to use the output artifact from the build stage as its input artifact.
4. CodeDeploy retrieves the code: When CodeDeploy executes its deployment action, it automatically pulls the deployment bundle (the "revision") from the S3 artifact bucket.
5. CodeDeploy agent: The CodeDeploy agent, which is running on each target EC2 instance, downloads the artifact from S3. It uses the `appspec.yml` file inside the artifact to determine how to proceed with the installation of the new application files.&#x20;
