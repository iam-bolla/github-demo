# Travifai DevOps Internship Assignment

## 🚀 Steps

### 1. Deploy App on EC2
- Launch Ubuntu EC2
- Install Node.js & PM2:
  ```bash
  sudo apt update -y
  sudo apt install -y nodejs npm
  sudo npm install -g pm2
  ```
---
Clone repo and run:

```bash
git clone https://github.com/<your-username>/<repo>.git
cd repo
npm install
pm2 start app.js --name app
```
Allow inbound traffic
open 3000

---
### 2. GitHub Actions Auto-Deploy
Configured .github/workflows/deploy.yml

On every push to main, code is deployed to EC2.

---
### 3.Access the application:
```bash
http://<EC2-public-ip>:3000
```
### 4.Create a bucket through aws cli by configuring acess keys and secret access key:
This bucket stores log files you can set cronjob 
PM2 saves logs by default in:
```bash
~/.pm2/logs/
```
For your app app, you’ll have two log files:

app-out.log → Standard output (console logs)

app-error.log → Error logs

 create bucket:
 ```bash
aws s3 mb s3://my-travifai-logs
```
Push logs to S3 manually
```bash
aws s3 cp ~/.pm2/logs/app-out.log s3://my-travifai-logs/
aws s3 cp ~/.pm2/logs/app-error.log s3://my-travifai-logs/
```
you can set cronjob here which syncs your logs according the time you set




