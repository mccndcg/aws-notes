# Access Compute Engine via VS Code

```sh
gcloud projects list
gcloud config set project PROJECT_ID
gcloud compute config-ssh
```

Install Remote—SSH: In VS Code, go to the Extensions view (Ctrl+Shift+X) and install the "Remote - SSH" extension.

**How to connect**

1. Open the Remote Explorer in VS Code by clicking the remote icon in the Activity Bar or by searching for "Remote Explorer" in the Command Palette (Ctrl+Shift+P).
2. In the Remote Explorer, you will see your GCE instances listed under the "SSH" section.
3. Click the "Connect to Host" icon next to your desired VM instance.
