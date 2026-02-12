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

## ✅ CI/CD Website Project Steps (Short)

### 1) Create a GitHub Repository
- Create a new GitHub repo (**public or private**)
- Upload your website files:
  - `index.html`
  - `style.css`

📌 **Frontend code reference:**  
Use the files already included in this repository:
- `index.html`
- `style.css`

---

### 2) Create an S3 Bucket (for Website Hosting)
- Go to **Amazon S3 → Create bucket**
- Example bucket name: `my-cicd-website-bucket`
- Keep the bucket in the **same region** where you will create the pipeline (example: `us-east-1`)

⚠️ **Important:**  
Do **NOT** upload website files manually in this bucket.  
The pipeline will deploy the files automatically.

---

### 3) Enable Static Website Hosting
Go to:

**S3 → Your Bucket → Properties → Static website hosting**

Enable it and set:

- **Index document:** `index.html`
- (Optional) **Error document:** `index.html`

⚠️ Important rule (to avoid the error we faced):  
✅ `index.html` must be at the **ROOT** of the bucket  
❌ Do not keep it inside a folder like: `project/index.html`

---

### 4) Make the Bucket Public (Only for Website Hosting)
You must allow public access so users can open the website.

#### A) Disable Block Public Access
Go to:

**S3 → Bucket → Permissions → Block public access**

- Uncheck **Block all public access**
- Save changes

#### B) Add Bucket Policy (Public Read)
Go to:

**S3 → Bucket → Permissions → Bucket policy**

📌 Add a public-read policy  
(**For policy JSON, refer to the bucket policy given above in this repository / notes**)

---

### 5) Create a CodePipeline
Go to:

**AWS CodePipeline → Create pipeline**

#### A) Pipeline Settings
- Pipeline name: `github-auto-deploy` (or any name you want)
- Service role: **New service role** (recommended)

---

#### B) Source Stage (IMPORTANT)
- Source provider: **GitHub (via GitHub App)**
- Click: **Connect to GitHub**
- Connection name: you can type any name  
  Example: `github-connection-cicd`

✅ Important:
- Install/Authorize the GitHub App (required)
- Select your repository + branch (example: `main`)

⚠️ If repo list is not showing:
- Your GitHub App is not installed/authorized properly

---

#### C) Build Stage (Optional)
You can:
- **Skip build stage** (for simple HTML/CSS websites)

OR

Use:
- Build provider: **AWS CodeBuild** (recommended for advanced workflows)

---

#### D) Deploy Stage (IMPORTANT)
- Deploy provider: **Amazon S3**
- Bucket: select your **website hosting bucket**
- Enable: ✅ **Extract file before deploy**

This is mandatory so your files deploy correctly.

---

### 6) Confirm Pipeline Success
After creating, you will see a pipeline diagram:

- ✅ Source should turn **green**
- ✅ Deploy should turn **green**

If Deploy is red:
- Usually bucket permission / artifact extraction issue

---

### 7) Test Website
Go to:

**S3 → Bucket → Properties → Static website hosting**

Copy the **Website endpoint URL**  
Open it in browser → your website should load.

---

### 8) Auto-Deploy Test (Final Confirmation)
- Make a change in `index.html`
- Push it to GitHub
- CodePipeline will run automatically
- Refresh your website → changes will appear

---

## ⚠️ Important Notes (Avoid Common Errors)

✅ Keep `index.html` at bucket root  
❌ Do not keep it like: `project/index.html`

✅ Do not upload website files manually in the S3 bucket  
Pipeline should deploy everything automatically

✅ Always enable:
- Bucket public read policy
- Extract file before deploy

---

## 👤 Author

**Umesh Saini**  
AWS Project

---
