# Car Doc Client Configuration

Client-specific content and deployment records for Car Doc.

Do not store secrets, passwords, database URLs, Supabase service keys, or private customer data here.

## Public SEO origin

Configure the production Vercel project with:

`NEXT_PUBLIC_SITE_URL=https://cardoc-rho.vercel.app`

This is the explicit canonical origin for the PlumWorks public pages. Do not derive it
from `VERCEL_URL`, use a preview deployment URL, or point it at the separately managed
`subbuscardoc.com` website. A future custom-domain change requires updating this
configuration value only.
