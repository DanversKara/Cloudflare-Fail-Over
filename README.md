# Cloudflare-ReRoute-Server-Down-to-another-server
redirect visitors to a backup server when the primary is unreachable

this is the cheap way.. poor mans fail over

1. Goto Cloudflare Workers & Pages
2. click on Create a Worker
3. click on Start with Hello World!
4. call it / name it: domain_failover.(gray out domain you cant edit *username)
5. click on deploy
6. on GitHub look for file EDIT_CODWE.txt
7. go back to cloudflare and click on the worker you named domain_failover.(gray out domain you cant edit *username)
8. edit the code

look for
text.includes("404") ||
        text.includes("502") ||
        text.includes("Bad Gateway") ||
        text.includes("nginx")

return fetch("https://karas-page-home.pages.dev");

const origin = "http://karas.page";

9. change the code to match your specs
so replace 502, Bad Gateway, Nginx, 404, with what you want cloudflare to search for.

10. replace cloudflare Workers & Pages domain with your domain of the backup website domain -> fail over domain return fetch("https://karas-page-home.pages.dev");
11. replace domain http://karas.page with your live domain all visitors see -> const origin = "http://karas.page";
12. Add a Trigger
- go back to domain_failover.(gray out domain you cant edit *username) from step 4
13. goto settings and look for Trigger Events
14. click +Add
15. Cron Triggers
16. Execute Worker every Minute(s)
17. every 1
18. click Add
19. Trigger Events should look like

Type
Handler
Details
Cron
scheduled()
*/1 * * * *
Schedule:Every minute View events
Next:Thu, 12 Mar 2026 00:54:00

20. go disconnect connection to live server/domain and after 1 minute go see if backup server is live from fail over.
