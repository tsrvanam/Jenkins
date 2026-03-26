# 🚀 Jenkins + GitHub Webhook Setup Guide

This guide explains how to configure Jenkins to automatically trigger builds when code is pushed to GitHub.

---

## 📌 Step 1: Ensure Jenkins is Reachable

Before configuring anything:

Jenkins must be accessible via a URL:

```
http://<your-server-ip>:8080
```

✅ Example:
```
http://3-12-34-56-78:8080
```

---

## ⚙️ Step 2: Configure Jenkins Job

Go to your Jenkins **Pipeline Job → Configure**

### 🔹 Source Code Configuration (IMPORTANT)

If using **Pipeline from SCM**:

- **Repository URL:**
```
https://github.com/your-username/your-repo.git
```

- **Branch:**
```
*/main
```

---

### 🔹 Enable Build Trigger

Check this option:

```
GitHub hook trigger for GITScm polling
```

👉 This is the **key setting** that allows Jenkins to listen to GitHub events.

---

## 🔗 Step 3: Add Webhook in GitHub

Go to your GitHub repository:

```
Repo → Settings → Webhooks → Add webhook
```

### Fill the following fields:

#### 🔹 Payload URL
```
http://<jenkins-url>/github-webhook/
```

✅ Example:
```
http://3-12-34-56-78:8080/github-webhook/
```

---

#### 🔹 Content Type
```
application/json
```

---

#### 🔹 Secret (Optional but Recommended)

- Add a secret string  
- Use the same secret in Jenkins (if configured)

---

#### 🔹 Events

Select:
```
Just the push event
```

👉 This is enough for basic CI/CD pipelines.

---

#### 🔹 Active

✔️ Keep this checked

Click:
```
Add webhook
```

---

## 🧪 Step 4: Test the Webhook

### Option 1: Push Code

```bash
git add .
git commit -m "test webhook"
git push origin main
```

---

### Option 2: Manual Test

Go to:
```
GitHub → Settings → Webhooks → Select your webhook → Recent Deliveries
```

---

## ✅ Step 5: Verify

### In GitHub:
- Status should be:
```
200 OK
```

### In Jenkins:
- Your job should trigger automatically 🎉

---

## 🎯 Summary

- Jenkins listens using webhook endpoint  
- GitHub sends event on every push  
- Jenkins triggers pipeline automatically  

---

## 🚀 You're Done!

You now have a fully automated CI trigger using Jenkins + GitHub Webhooks.
