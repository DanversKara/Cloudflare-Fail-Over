# Cloudflare-ReRoute-Server-Down-to-another-server
redirect visitors to a backup server when the primary is unreachable

this is the cheap way.. poor mans fail over

1. Goto Cloudflare Workers & Pages
2. click on Create a Worker

4. click on Start with Hello World!

6. call it / name it: domain_failover.(gray out domain you cant edit *username)

8. click on deploy

9. on GitHub look for file EDIT_CODE.txt it will then say to look for EDIT_Code.zip, github keeps chaning the code, so i had to zip it.
    Also cloudflare will also edit the code once you paste it into edit code box - so just edit the urls/code on a notepad, then past it into the edit code box.

11. go back to cloudflare and click on the worker you named domain_failover.(gray out domain you cant edit *username)

12. edit the code by clicking on EDIT CODE BUTTON

13. the EDIT_Code.txt/zip - edit it outside cloudflare how you need it with the correct urls, then paste into edit code box but you must first change the domains/urls as it i have it default to mine.
look for
<p>const backup = "https://karas-page-home.pages.dev";</p>
<p></p>backupUrl.hostname = "karas-page-home.pages.dev";</p>
and replace the code with your cloudflare url as they are mine as default

15. replace cloudflare Workers & Pages domain with your domain of the backup website domain -> fail over domain return fetch("https://karas-page-home.pages.dev");
16. replace domain http://karas.page with your live domain all visitors see -> const origin = "http://karas.page";

17. under Domains & Routes click on +Add then Zone is the default domain, then Route enter your domain DO NOT ADD /* then Failure Mode click on FAIL OPEN (PROCEED)
18. go disconnect connection to live server/domain and after 1 minute go see if backup server is live from fail over.
