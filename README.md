# IMPORTANT LEGAL NOTICE
All malicious code analyzed in this repository is being done so under Fair Use. If you live in other countries, please be aware of the laws about infringing on the copyright of malware developers.
GETTING A SAMPLE: https://shaderblox.xyz/ is where you can get the latest malware sample! Currently, their file host (Storj) has removed the file by my request, so it might not be up now :)
# Step 1.
The malware is packed using a custom version of InnoSetup. Currently, it can only be unpacked by ONE PROGRAM:
This is the program: https://github.com/jrathlev/InnoUnpacker-Windows-GUI/blob/master/innounp-2/bin/innounp-2.zip
It will ask for a PASSWORD when extracting. This is a Technological Protection Measure implemented by the malware authors to limit access to their malware to real victims, and for legal reasons under section 1201 of the Digital Millenium Copyright act, I cannot say how to get this password. However, I HOPEFULLY can say that during the execution flow, it is passed as a cli parameter to another executable, so a sandbox might be your best friend
Once you have the password and have extracted the innosetup, go to the "{app}" directory.
# Step 2.
Use pkg-unpacker to unpack the "updater.exe"
# Step 3.
Now, you will have to find the file "snapshot" -> "STEALER" -> "dist" -> "app.js". This is a heavily obfuscated compiled javascript file containing the malware
# Step 4.
Remove the first layer of obfuscation:
```const crypto = require('crypto');

const password = "<Password found in the file, starts with a V, redacted under section 1201>";
const salt = Buffer.from("<Salt starting with an A, redacted under section 1201>", "base64");
const iv = Buffer.from("<IV starting with N, redacted under section 1201>", "base64");
const encrypted = "giant base64 blob found using strings on the app.js";

const key = crypto.pbkdf2Sync(password, salt, 100000, 32, 'sha512');
const decipher = crypto.createDecipheriv('aes-256-cbc', key, iv);
let decrypted = decipher.update(encrypted, 'base64', 'utf8');
decrypted += decipher.final('utf8');

console.log(decrypted);
```
That will output the next stage
# Step 5.
This stage is obfuscated using obfuscator.io, all that I can say is that https://obf-io.deobfuscate.io/ is a completely unrelated but useful site
# Step 6.
The C2 is api.lyra-connect.us. Hopefully this article will be able to get AV companies to act, currently only enterprise providers and one consumer provider (Kaspersky) detect the C2, and Kaspersky is the only one to detect the malicious file.

If you need any copyright permissions from the malware author, you can contact them with their contacts, shown below. Brazilian Police, take note of this!
<img width="670" height="481" alt="image" src="https://github.com/user-attachments/assets/ff4dd0ff-bfb4-40be-b74f-c6765b4215f3" />
