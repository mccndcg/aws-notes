# AMI w/ Code Deploy

Refer to: [#codepipeline-greater-than-codedeploy-greater-than-ec2](../../../aws-code/aws-codedeploy/questions.md#codepipeline-greater-than-codedeploy-greater-than-ec2 "mention")

* Create an Image Builder pipeline: Use the EC2 Image Builder console to create a new image pipeline. This pipeline will define how to build your AMI.
* Define a recipe: In the pipeline configuration, define an "image recipe" that specifies the base AMI (your current common AMI) and a "component" for installing the CodeDeploy agent.
* Run the pipeline: Run the Image Builder pipeline. It will automatically launch an instance, execute the components (including installing the CodeDeploy agent), and create a new, updated AMI for you.
* Update the Auto Scaling group: Similar to the manual method, update your Auto Scaling group's launch template to use the new AMI created by the pipeline.&#x20;
