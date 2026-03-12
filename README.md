# Cloudflare ReRoute: Server Down Failover

Redirect visitors to a backup server when the primary server is unreachable.  
This is a “poor man’s” failover solution using **Cloudflare Workers & Pages**. 

**NOTICE:** You are only allowed so much free usage before they want you to upgrade to a paid plan when visitors need to hit your failover pages. So make sure you configure the domains to block a lot of Ai / Crawler / Bot / Under Attack Traffic, so you dont need to upgrade.

**THIS WILL NOT WORK FOR ALL DOMAINS**
some websites like YunoHost with its SSO, i cant seem to get it to work, So if you find away to get it to work with sites like that, Let me know.

---

## Steps to Set Up

### 1. Create your free page (skip this if you wanna have fail backup go somewhere else)
1. Go to [Cloudflare Workers & Pages](https://workers.cloudflare.com/)  
2. Click **Create a Worker**  
3. Click on: Looking to deploy Pages? Get started
4. Pick from Import or Drag (upload your files)
5. Name your worker: `domain_failover_page.*username*` (the domain part is grayed out and cannot be edited)  
6. now make sure you copy the url to use in the EDIT_Code.txt later and Edit Code Box. `EDIT_Code.txt: const backup = "http://your-live-domain.com";`

---

### 2. Create a Cloudflare Worker
1. Go to [Cloudflare Workers & Pages](https://workers.cloudflare.com/)  
2. Click **Create a Worker**  
3. Choose **Start with Hello World!**  
4. Name your worker: `domain_failover_code.*username*` (the domain part is grayed out and cannot be edited)  
5. Click **Deploy**
6. Now make sure you copy the url to use in the EDIT_Code.txt later and Edit Code Box. `EDIT_Code.txt: backupUrl.hostname = "your-cloudflare-backup-pages.pages.dev";`

---

### 3. Go back to Cloudflare and select your worker (`domain_failover.*username*`)
1. Click on Settings Tab, look for Domains & Routes
   - click on +Add
   - Pick ROUTE
   - Pick Zone, find the live domain you want users togo to when domain is live.
   - Route Box: type in your Domain example/* (must put /* at the end) sometimes you might *.example/* - this depands on what you are doing on the live server.
   - Failure Mode, Pick Fail Open (proceed)
   - Then Update Route.

---
### 4. Edit the Worker Code
1. On GitHub, look for the file `EDIT_CODE.txt` (it may refer to `EDIT_Code.zip`)  
   - GitHub changes code formatting frequently, so the zip version is recommended.  
   - Cloudflare may also auto-format the code when pasted, so it’s best to edit in Notepad or another text editor first.  

2. Go back to Cloudflare and select your worker (`domain_failover.*username*`)  
3. Click **Edit Code**  

---

### 5. Customize the Code
1. Open `EDIT_Code.txt` or the unzipped `EDIT_Code` folder.  
2. Replace the default backup and live URLs with your own:

```javascript
// Replace with your live domain (all visitors see this)
const backup = "http://your-live-domain.com";

// Replace with your backup Cloudflare Pages domain
backupUrl.hostname = "your-cloudflare-backup-pages.pages.dev";

// Also Change the text from NPM-LOCAL and Bad Gateway, to whatever you want Cloudflare to detect as in look for to discover the page isnt live anymore. also ( ||) is needed do not alter - ask Ai to better re-write your code if you need to add or remove  ||.
          text.includes("NPM-LOCAL") ||
          text.includes("Bad Gateway")
