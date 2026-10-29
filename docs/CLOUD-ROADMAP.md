# Cloud roadmap

ClassOf5 OS is lightweight and portable: it runs anywhere PHP and MySQL run, which kept launch fast and the platform cost-efficient to run. The roadmap below adds cloud automation, resilience and scale around it in small steps, each useful on its own. I'll update this page as each one lands.

| # | Step | Why | Status |
|---|---|---|---|
| 1 | **CI/CD with GitHub Actions:** tests on every push; automatic staging deploys; gated, approved production deploys | Catch problems before staging; repeatable releases | ✅ Done (29 Oct 2026): see [CI.md](CI.md) |
| 2 | **Off-site backups:** copy the nightly database backup to Azure Blob Storage (or AWS S3) with lifecycle rules (30 days hot, then archive) | Backups survive a hosting failure | Planned |
| 3 | **Infrastructure as code:** Terraform for the storage account or bucket, its least-privilege access key or role, and alerts | Repeatable, reviewable infrastructure | Planned |
| 4 | **Containers:** a Docker Compose stack (PHP + Apache, MySQL, mail catcher) mirroring production | One-command local and test environments | Planned |
| 5 | **Monitoring:** hourly uptime checks of the key pages, database, scheduled jobs, daily backup and SSL certificates, with email alerts | Know before families do | ✅ Done (29 Oct 2026): see [OPERATIONS.md](OPERATIONS.md#monitoring) |
| 6 | **Migration design (architecture decision record):** Azure App Service + Azure Database for MySQL, or AWS Lightsail/EC2 + RDS + CloudFront; cost, risk and cut-over plan | Ready to scale with demand (more schools, more learners) | Planned |

Skills this exercises: Azure (AZ-104), AWS (Solutions Architect Associate), Terraform, GitHub Actions, Docker, monitoring and cost planning.
