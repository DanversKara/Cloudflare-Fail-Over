# Cloudflare-ReRoute-Server-Down-to-another-server
redirect visitors to a backup server when the primary is unreachable

1. Goto Cloudflare Workers & Pages
Build & deploy serverless functions, sites, and full-stack applications.
2. click on Create a Worker
3. click on Start with Hello World!
4. call it domain_failover.
5. deploy
6. Edit Code Button top right
7. Paste Code from File (Edit_Code.txt)
8. change
text.includes("404") ||
        text.includes("502") ||
        text.includes("Bad Gateway") ||
        text.includes("nginx")

to match what you want it to detect

9. create another worker page with backup of your website or goto step 10.

10. (this is the failover domain)
edit       return fetch("https://karas-page-home.pages.dev");

replace domain with your worker page domain or your new fail over domain

11. (this is live domain)
edit     const origin = "http://karas.page";

with your domain that all visitors goto when its working

12. click top right Deply button

13. that should be it
