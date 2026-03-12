# Cloudflare ReRoute: Server Down Failover

Redirect visitors to a backup server when the primary server is unreachable.  
This is a “poor man’s” failover solution using **Cloudflare Workers & Pages**.

---

## Steps to Set Up

### 1. Create a Cloudflare Worker
1. Go to [Cloudflare Workers & Pages](https://workers.cloudflare.com/)  
2. Click **Create a Worker**  
3. Choose **Start with Hello World!**  
4. Name your worker: `domain_failover.*username*` (the domain part is grayed out and cannot be edited)  
5. Click **Deploy**  

---

### 2. Edit the Worker Code
1. On GitHub, look for the file `EDIT_CODE.txt` (it may refer to `EDIT_Code.zip`)  
   - GitHub changes code formatting frequently, so the zip version is recommended.  
   - Cloudflare may also auto-format the code when pasted, so it’s best to edit in Notepad or another text editor first.  

2. Go back to Cloudflare and select your worker (`domain_failover.*username*`)  
3. Click **Edit Code**  

---

### 3. Customize the Code
1. Open `EDIT_Code.txt` or the unzipped `EDIT_Code` folder.  
2. Replace the default backup and live URLs with your own:

```javascript
// Replace with your live domain (all visitors see this)
const origin = "http://your-live-domain.com";

// Replace with your backup Cloudflare Pages domain
backupUrl.hostname = "your-cloudflare-backup-pages.pages.dev";

// Also Change the text from NPM-LOCAL and Bad Gateway, to whatever you want Cloudflare to detect as in look for to discover the page isnt live anymore. also ( ||) is needed do not alter - ask Ai to better re-write your code if you need to add or remove  ||.
          text.includes("NPM-LOCAL") ||
          text.includes("Bad Gateway")
