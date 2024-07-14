# Verifying SSH signatures

Most of my projects use SSH signatures for digitally signing the downloads.

To verify the signature of a file, run the two commands listed below. This will first save the trusted key to a file named `chenxiaolong_trusted_keys` and then use it to verify the signature. Make sure to replace `<filename>` with the actual filename.

For Unix-like systems and Windows (Command Prompt):

```bash
echo chenxiaolong ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDOe6/tBnO7xZhAWXRj3ApUYgn+XZ0wnQiXM8B7tPgv4 > chenxiaolong_trusted_keys

ssh-keygen -Y verify -f chenxiaolong_trusted_keys -I chenxiaolong -n file -s <filename>.sig < <filename>
```

For Windows (PowerShell):

```powershell
echo 'chenxiaolong ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDOe6/tBnO7xZhAWXRj3ApUYgn+XZ0wnQiXM8B7tPgv4' | Out-File -Encoding ascii chenxiaolong_trusted_keys

Start-Process -Wait -NoNewWindow -RedirectStandardInput <filename> ssh-keygen -ArgumentList "-Y verify -f chenxiaolong_trusted_keys -I chenxiaolong -n file -s <filename>.sig"
```

If the file is successfully verified, the output will be:

```
Good "file" signature for chenxiaolong with ED25519 key SHA256:Ct0HoRyrFLrnF9W+A/BKEiJmwx7yWkgaW/JvghKrboA
```
