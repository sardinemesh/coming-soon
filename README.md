# SardineMesh holding page

A static, dependency-free page for GitHub Pages, using the approved mesh-tail brand assets. The `CNAME` file targets `sardinemesh.com`.

## Publish

1. Create a separate public repository in the `sardinemesh` organization (for example, `coming-soon`). Put the contents of this directory at the repository root on `main`.
2. In repository **Settings → Pages**, choose **Deploy from a branch**, `main`, `/ (root)`. Set the custom domain to `sardinemesh.com`. The committed `CNAME` file declares the same domain.
3. In the Route 53 hosted zone for `sardinemesh.com`, replace any existing apex A/AAAA records that direct the root domain elsewhere with the GitHub Pages records below. Leave unrelated records (MX, TXT, and the `intel` subdomain) alone. If an apex DNS record already serves another site, changing it will move that site.
4. Optionally point `www.sardinemesh.com` to `sardinemesh.github.io` with a CNAME. GitHub Pages will redirect `www` to the configured apex domain.
5. Verify the domain in the GitHub organization’s **Settings → Pages** using the TXT record GitHub supplies. Once DNS and the certificate are ready, turn on **Enforce HTTPS** in the repository’s Pages settings.

| Name | Type | Value |
| --- | --- | --- |
| `sardinemesh.com` | A (one record with four values) | `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` |
| `www.sardinemesh.com` | CNAME (optional) | `sardinemesh.github.io` |

GitHub also supports four AAAA records for IPv6, but they are optional. The root domain cannot use an ordinary CNAME in Route 53. Do not point `intel.sardinemesh.com` to Pages unless replacing the application there is intended. Avoid wildcard DNS records.

Check DNS with `dig sardinemesh.com A +short` and `dig www.sardinemesh.com CNAME +short`; then visit `https://sardinemesh.com/` after GitHub reports the deployment and HTTPS certificate as ready. DNS and HTTPS provisioning can take up to 24 hours.

The page uses only relative asset paths, so it can also be previewed by opening `index.html` locally or with `python3 -m http.server` in this directory.

Official guides: [GitHub custom domains](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site), [GitHub domain verification](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages).
