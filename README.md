# GGP Flask Server

Backend server for your GGP Browser with file uploads, zip creation, and code execution.

## Features

✅ **File Uploads** - Single or multiple files
✅ **Zip Files** - Upload, extract, and create zips
✅ **Code Execution** - Run Python code safely
✅ **File Management** - Save, list, and organize files
✅ **Git Integration** - Push to GitHub (needs credentials)
✅ **Consciousness API** - Field calculations

## Quick Start

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Run Server
```bash
python ggp_server.py
```

Server runs on: `http://localhost:5000`

## API Endpoints

### File Upload
```bash
# Upload single file
curl -X POST -F "files=@myfile.py" http://localhost:5000/api/upload

# Upload multiple files
curl -X POST -F "files=@file1.py" -F "files=@file2.py" http://localhost:5000/api/upload
```

### Upload & Extract Zip
```bash
curl -X POST -F "file=@project.zip" http://localhost:5000/api/upload/zip
```

### Create Zip
```bash
curl -X POST http://localhost:5000/api/zip/create \
  -H "Content-Type: application/json" \
  -d '{
    "project_id": "my_consciousness_project",
    "files": ["uploads/field.py", "uploads/oracle.py"]
  }'
```

### Download Zip
```bash
curl http://localhost:5000/api/zip/download/my_consciousness_project -o project.zip
```

### Run Python Code
```bash
curl -X POST http://localhost:5000/api/run \
  -H "Content-Type: application/json" \
  -d '{
    "code": "print(\"Hello from consciousness field\")",
    "timeout": 5
  }'
```

### Save Code
```bash
curl -X POST http://localhost:5000/api/save \
  -H "Content-Type: application/json" \
  -d '{
    "filename": "consciousness_field.py",
    "code": "# Your code here",
    "folder": "my_project"
  }'
```

### List Files
```bash
curl http://localhost:5000/api/files
```

### Git Push (Simulated)
```bash
curl -X POST http://localhost:5000/api/git/push \
  -H "Content-Type: application/json" \
  -d '{
    "repo": "https://github.com/youruser/yourrepo",
    "branch": "main",
    "message": "Update consciousness fields"
  }'
```

### Consciousness Field Calculation
```bash
curl -X POST http://localhost:5000/api/consciousness/field \
  -H "Content-Type: application/json" \
  -d '{
    "field_type": "Mind",
    "chart_system": "sidereal"
  }'
```

## Connect to Your Browser

Update your GGP browser to point to this server:

```javascript
// In your browser JavaScript
const API_URL = 'http://localhost:5000';

// Upload file example
async function uploadFile(file) {
    const formData = new FormData();
    formData.append('files', file);
    
    const response = await fetch(`${API_URL}/api/upload`, {
        method: 'POST',
        body: formData
    });
    
    return await response.json();
}

// Run code example
async function runCode(code) {
    const response = await fetch(`${API_URL}/api/run`, {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({code, timeout: 5})
    });
    
    return await response.json();
}
```

## Folder Structure

```
.
├── ggp_server.py       # Main server
├── requirements.txt    # Dependencies
├── uploads/           # Uploaded files (auto-created)
├── projects/          # Saved projects (auto-created)
└── temp/              # Temporary files (auto-created)
```

## Security Notes

⚠️ **This is a development server**
- Don't expose directly to internet
- Add authentication for production
- Sanitize file uploads
- Limit code execution scope
- Add rate limiting

## Real Git Integration

To add real Git pushing, install GitPython:

```bash
pip install GitPython
```

Then update the `git_push` endpoint:

```python
import git

@app.route('/api/git/push', methods=['POST'])
def git_push():
    data = request.json
    repo_path = data.get('repo_path', './projects')
    
    repo = git.Repo(repo_path)
    origin = repo.remote('origin')
    origin.push()
    
    return jsonify({'success': True})
```

## Connect with Your Gun (Deploy) 🔫

### Local Network
```bash
# Run on your network
python ggp_server.py
# Access from phone: http://YOUR_IP:5000
```

### Deploy to Cloud
- **Heroku**: `git push heroku main`
- **Railway**: Connect GitHub repo
- **DigitalOcean**: Deploy as Python app
- **Replit**: Upload and run

Your consciousness tools are ready to go live. 🌌
