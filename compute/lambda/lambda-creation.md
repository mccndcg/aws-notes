# Lambda Creation

{% hint style="info" %}
This guide assumes you have an AWS account and have already created the necessary pre-existing resources, such as an IAM execution role, VPC, and subnets.&#x20;
{% endhint %}

**Step 1: Navigate to the Lambda Console**

1. Sign in to the AWS Management Console.
2. In the search bar at the top, type `Lambda` and select AWS Lambda from the results.
3. On the Lambda dashboard, click the Create function button.&#x20;

***

**Step 2: Define basic function information**

1. On the Create function page, select the Author from scratch option.
2. In the Basic information section:
   * Function name: Enter a descriptive name for your function (e.g., `MyVPCFunction`).
   * Runtime: Choose the programming language for your function code (e.g., `Python 3.12`).
   * Architecture: Leave this as the default (`x86_64`) or choose `arm64` if preferred.
3. In the Permissions section:
   * Expand the Change default execution role menu.
   * Select Use an existing role.
   * From the dropdown, select the IAM role you have already prepared for this function. This role must have permissions to run Lambda functions and access any other required AWS services.
4. Click Create function.&#x20;

***

**Step 3: Add your code**

{% hint style="info" %}
_After the function is created, you will be taken to its configuration page._
{% endhint %}

1. Scroll down to the Code tab.
2. You can either:
   * Edit inline: Write or paste your code directly into the editor. This is ideal for simple functions.
   * Upload from: If your function requires dependencies, you will need to package your code into a `.zip` file. Click the Upload from button and select the `.zip` option.
3. After editing or uploading, click Deploy to save your changes.&#x20;

***

**Step 4: Configure VPC access**

{% hint style="info" %}
_This step is for functions that need to access resources within a VPC._
{% endhint %}

1. Go to the Configuration tab for your function.
2. Select VPC from the left-hand menu and click the Edit button.
3. Under VPC, select the target VPC from the dropdown.
4. Under Subnets, select the private subnets you want the function to use. Choosing multiple subnets across different Availability Zones is a best practice for high availability.
5. Under Security groups, select the security groups that control the network traffic for your function.
6. Click Save.&#x20;

***

**Step 5: Test your function**

1. Click the Test tab at the top of the function page.
2. Click Create new test event.
3. Give your test event a name and configure the test payload in JSON format, which will be passed to your function as the `event` object.
4. Click Save, and then click Test to run your function.
5. Review the Execution results tab to see the output, logs, and billing details.&#x20;

***

**Step 6: Add a trigger**

{% hint style="info" %}
If your function is not for manual testing, you'll need to configure a trigger to invoke it automatically.
{% endhint %}

1. Go to the Function overview section of your function's page.
2. Click the Add trigger button.
3. From the trigger source list, choose the appropriate AWS service (e.g., API Gateway for HTTP requests, S3 for file uploads, EventBridge for scheduled tasks).
4. Configure the settings for the trigger and click Add.&#x20;
