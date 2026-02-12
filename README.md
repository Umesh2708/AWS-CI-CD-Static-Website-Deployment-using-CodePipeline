# AWS CI/CD Static Website Deployment (CodePipeline + S3)

A cloud-based DevOps project where **every GitHub code update automatically deploys the latest website version** using **AWS CodePipeline**.

---

## 📌 Project Idea (Short Intro)

You will build a system where whenever you push your website code to GitHub, AWS will automatically build and deploy the latest version to your live website.

---

## 🔁 How It Works (Simple Flow)

1. You create a simple website (**HTML / CSS / JS**)
2. You upload the code to **GitHub**
3. You create an **AWS CodePipeline**
4. Pipeline automatically:
   - pulls code from GitHub  
   - runs build using **CodeBuild** *(optional but recommended)*  
   - deploys the final files to **S3 Static Website Hosting**

---

## 🌍 Final Output

You get a **live hosted website link**, and every time you update code in GitHub, it updates automatically.

---

## 🧰 AWS Services Used

- **Amazon S3** (Static Website Hosting)
- **AWS CodePipeline** (CI/CD automation)
- **AWS CodeBuild** *(optional but recommended)*
- **AWS IAM** (Permissions)
- **GitHub** (Source code repository)

---

📌 **Frontend code reference:**  
Use the files already included in this repository:
- `index.html`
- `style.css`

---

## ✅ CI/CD Website Project Steps (Short)

### 1) Create a GitHub Repository
- Create a new repo (public or private)
- Upload your website files:
  - `index.html`
  - `style.css`
  - `script.js`

---

### 2) Create an S3 Bucket
- Create a bucket (example: `my-cicd-website-bucket`)
- Keep the bucket in the same region where you will create the pipeline

---

### 3) Enable Static Website Hosting
Go to:
- **S3 → Your Bucket → Properties → Static website hosting**
- Enable it
- Set:
  - **Index document:** `index.html`
  - (Optional) **Error document:** `index.html`

---

### 4) Make the Bucket Public (Only for Website Hosting)
You must allow public access so users can open the website.

Go to:
- **Permissions → Block public access**
  - Uncheck **Block all public access**
- Add a **Bucket Policy** that allows public read access for website files.

---

### 5) Create a CodePipeline
Go to:
- **AWS CodePipeline → Create pipeline**

Set stages like this:

#### ✅ Source Stage
- Source provider: **GitHub**
- Select your repo + branch (example: `main`)

#### ✅ Build Stage (Optional but Recommended)
- Build provider: **AWS CodeBuild**
- Create a new build project
- Output: build artifacts

#### ✅ Deploy Stage
- Deploy provider: **Amazon S3**
- Bucket: your static website bucket
- Enable: **Extract file before deploy**

---

### 6) Test the Deployment
- Open the S3 static website URL
- You should see your website live

---

### 7) Auto Deployment Test
- Make a change in `index.html`
- Push it to GitHub
- CodePipeline runs automatically
- Website updates automatically 🎉

---

## ⚠️ Important Notes

- Make sure **S3 Static Website Hosting** is enabled.
- Make sure the bucket is **public readable** for website access.
- In CodePipeline deploy stage, always enable:
  ✅ **Extract file before deploy**
- CodeBuild is optional, but recommended if you want a professional CI/CD flow.

---

## 👤 Author

**Umesh Saini**  
AWS Project

---
