
# 📘 Node.js Deploy Example – Project Documentation

A simple Node.js web server app deployed on an AWS EC2 instance. This project demonstrates the fundamental process of deploying a Node.js app on a cloud server.

---

## 📁 Project Structure

```
nodejs-deploy-example/
├── index.js        # Main Node.js server script
├── README.md       # Project documentation
```

---

## ⚙️ Requirements

- Node.js (v18+)
- npm (v10+)
- Git
- AWS EC2 Instance (Ubuntu)
- Nginx (optional for reverse proxy)
- PM2 (optional for process manager)

---

## 🚀 Setup Instructions

### 1. Clone the GitHub Repository

```bash
git clone https://github.com/GeigerJR/nodejs-deploy-example.git
cd nodejs-deploy-example
```

---

### 2. Install Node.js and npm

```bash
sudo apt update
sudo apt install -y nodejs npm
```

---

### 3. Create the Node.js Server

```bash
nano index.js
```

Paste the code below:

```javascript
const http = require('http');
const PORT = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.end('Hello from your Node.js server on EC2!');
});

server.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}/`);
});
```

Save and exit: `CTRL + O`, `ENTER`, then `CTRL + X`

---

### 4. Start the Server

```bash
node index.js
```

Then visit:

```
http://<your-ec2-public-ip>:3000
```

---

## 📦 Optional: Use PM2 for Process Management

Install and use PM2 to keep the app running even after terminal logout:

```bash
sudo npm install -g pm2
pm2 start index.js
pm2 save
pm2 startup
```

---

## 🌐 Optional: NGINX Reverse Proxy Setup

**Install Nginx:**

```bash
sudo apt install nginx
```

**Configure reverse proxy:**

```bash
sudo nano /etc/nginx/sites-available/default
```

Replace the `location /` block:

```nginx
location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}
```

**Restart Nginx:**

```bash
sudo systemctl restart nginx
```

Visit your EC2 Public IP in the browser (`http://<your-ec2-ip>`).

---

## 📝 Update and Push README to GitHub

Create the README:

```bash
nano README.md
```

Paste in all content from this note, then:

```bash
git add README.md
git commit -m "Add full project documentation"
git push origin main
```

---

## 👤 Author

- GitHub: [GeigerJR](https://github.com/GeigerJR)

---

## 🏁 License

This project is licensed under the MIT License.
