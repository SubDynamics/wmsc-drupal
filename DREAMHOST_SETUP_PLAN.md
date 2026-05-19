# DreamHost Setup Plan (Drupal)

## Goal
Set up this Drupal site on DreamHost shared hosting with:
- **Production** at the primary domain (for example, `example.com`)
- **Staging** at a subdomain (for example, `staging.example.com`)

## 1) Prepare DreamHost and local prerequisites
1. Confirm DreamHost shared hosting access (panel + SSH/SFTP user).
2. Confirm domain DNS is managed and editable.
3. Ensure local tools are available for deployment and maintenance:
   - `git`
   - `composer`
   - `drush` (optional but recommended)
4. Decide deployment strategy:
   - Git-based deploy from this repository, or
   - Archive/upload build artifacts.

## 2) Create production site in DreamHost panel
1. In DreamHost panel, add a **Fully Hosted** domain for the primary domain.
2. Enable PHP 8.3+ for the domain.
3. Set web directory to this project’s document root (`web/`) in deployment layout.
4. Create a MySQL database + user for production.
5. Record securely:
   - DB name
   - DB user
   - DB password
   - DB host

## 3) Create staging site as subdomain
1. Add subdomain (for example, `staging.example.com`) as a separate **Fully Hosted** site.
2. Enable PHP 8.3+ for staging.
3. Use a separate web directory from production.
4. Create a separate MySQL database + user for staging.
5. Store staging DB credentials securely.

## 4) Configure repository-based deploy structure
1. Keep codebase shared by environment, but isolate writable files:
   - `web/sites/default/files` per environment
   - private files directory per environment (outside web root)
2. Ensure each environment has its own `settings.php` overrides (or include files) for:
   - Database credentials
   - Trusted host patterns
   - File paths
   - Environment flags
3. Do **not** commit secrets. Use DreamHost-managed files or environment-specific include files on server.

## 5) Deploy code to staging first
1. Deploy current branch to staging web directory.
2. Install dependencies on server (`composer install --no-dev -o`) if not prebuilt.
3. Set secure permissions:
   - Writable: files directories only
   - Non-writable: code files
4. Run Drupal install (new site) or import DB/config (existing site).
5. Run post-deploy commands:
   - `drush updb -y`
   - `drush cim -y` (if config-managed)
   - `drush cr`

## 6) Validate staging
1. Verify homepage, admin login, forms, and media uploads.
2. Verify email behavior (DreamHost SMTP/sendmail configuration).
3. Verify cron execution and caches.
4. Verify TLS certificate is active for staging subdomain.
5. Capture sign-off before production deploy.

## 7) Deploy to production (primary domain)
1. Put site in maintenance mode if needed.
2. Deploy same tested code version from staging.
3. Configure production `settings.php`/include with production DB + host settings.
4. Run post-deploy commands:
   - `drush updb -y`
   - `drush cim -y` (if used)
   - `drush cr`
5. Disable maintenance mode.

## 8) DNS and SSL cutover
1. Point primary domain DNS to DreamHost hosting if not already pointed.
2. Confirm DreamHost Let’s Encrypt certificate issuance for both:
   - `example.com`
   - `staging.example.com`
3. Force HTTPS redirect after certificates are active.

## 9) Backups, monitoring, and rollback
1. Enable automatic DreamHost database backups (or scheduled dumps).
2. Keep file backups for `sites/default/files` and private files.
3. Document rollback steps:
   - Re-deploy prior release
   - Restore prior DB backup
   - Clear caches
4. Set recurring checks for uptime, logs, and disk usage.

## 10) Ongoing workflow
1. Use staging for all updates first.
2. Promote only validated releases to production.
3. Keep core and dependencies updated via routine maintenance windows.
