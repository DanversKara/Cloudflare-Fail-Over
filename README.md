# Cloudflare-ReRoute-Server-Down-to-another-server
redirect visitors to a backup server when the primary is unreachable

this is the cheap way.. poor mans fail over

1. Goto Cloudflare Workers & Pages
2. click on Create a Worker

4. click on Start with Hello World!

6. call it / name it: domain_failover.(gray out domain you cant edit *username)
7. click on deploy

9. on GitHub look for file EDIT_CODWE.txt

11. go back to cloudflare and click on the worker you named domain_failover.(gray out domain you cant edit *username)
12. 
13. edit the code
look for
const backup = "https://karas-page-home.pages.dev";
backupUrl.hostname = "karas-page-home.pages.dev";
and replace the code with your cloudflare url as they are mine as default

14. replace cloudflare Workers & Pages domain with your domain of the backup website domain -> fail over domain return fetch("https://karas-page-home.pages.dev");
15. replace domain http://karas.page with your live domain all visitors see -> const origin = "http://karas.page";

20. under Domains & Routes click on +Add then Zone is the default domain, then Route enter your domain DO NOT ADD /* then Failure Mode click on FAIL OPEN (PROCEED)
21. go disconnect connection to live server/domain and after 1 minute go see if backup server is live from fail over.
