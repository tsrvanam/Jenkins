Step 1: Make sure Jenkins is reachable

Before touching GitHub:

Jenkins must be accessible via URL:
http://<your-server-ip>:8080

👉 Examples:

EC2: http://ec2-xx-xx-xx.compute.amazonaws.com:8080
Local → use ngrok:
ngrok http 8080

⚠️ If GitHub cannot reach Jenkins → webhook will FAIL

⚙️ Step 2: Enable GitHub integration in Jenkins

Go to:

Manage Jenkins → Configure System

Find: GitHub section
Click Add GitHub Server
Add credentials:
Kind: Username + Password OR Token
Use GitHub Personal Access Token

👉 This connects Jenkins with GitHub

🔑 Step 3: Generate GitHub Personal Access Token (PAT)

In GitHub:

Go to:
Settings → Developer Settings → Personal Access Tokens
Click Generate Token
Give permissions:
✅ repo
✅ admin:repo_hook
Copy token → add in Jenkins credentials
🧱 Step 4: Configure your Jenkins Job

Go to your pipeline job:

✔️ Source Code (VERY IMPORTANT)
If using Pipeline from SCM:

Repo URL:

https://github.com/your-username/your-repo.git

Branch:

*/main
✔️ Enable trigger

Check:

GitHub hook trigger for GITScm polling

👉 This is the key switch

🌐 Step 5: Add Webhook in GitHub

Now go to your repo in GitHub:

Path:

Repo → Settings → Webhooks → Add webhook

Fill these fields:
🔹 Payload URL:
http://<jenkins-url>/github-webhook/

Example:

http://ec2-12-34-56-78.compute.amazonaws.com:8080/github-webhook/
🔹 Content type:
application/json
🔹 Secret:

(optional but recommended)

Add same secret in Jenkins if configured
🔹 Which events?

Select:

Just the push event

👉 Enough for basic CI/CD

🔹 Active:

✔️ Keep checked

Click:

✅ Add webhook

🧪 Step 6: Test the Webhook
Option 1: Push code
git add .
git commit -m "test webhook"
git push origin main
Option 2: Manual test

In GitHub → Webhooks → click your webhook → Recent Deliveries

✅ Step 7: Verify
In GitHub:
Status should be:
200 OK
In Jenkins:
Job should trigger automatically 🎉
