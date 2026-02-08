# nginxVhost

A Python automation tool to quickly create and configure Nginx virtual hosts on Linux systems.

## Overview

This script automates the entire process of setting up a new Nginx virtual host, eliminating repetitive manual configuration steps. It handles vhost file creation, system directory setup, permission management, and Nginx configuration validation.

## Features

- **Automated vhost creation** - Generates Nginx configuration files from a template
- **Automatic placeholder replacement** - Replaces domain placeholder with your actual domain name
- **Sites-available/sites-enabled management** - Creates proper symlinks for Nginx vhost activation
- **Directory and permission setup** - Creates `/var/www/{domain}` directory with correct `nginx:nginx` ownership
- **Test page generation** - Creates a basic `index.html` file for testing
- **Configuration validation** - Runs `nginx -t` to verify configuration before reloading
- **Service reload** - Automatically reloads Nginx to apply changes
- **Colored status output** - Clear visual feedback for each step

## Template Features

The included Nginx configuration template (`template`) provides:
- **HTTPS redirect** - Automatically redirects HTTP traffic to HTTPS
- **SSL/TLS support** - Ready for SSL certificate configuration
- **Proxy headers** - Proper X-Forwarded headers for reverse proxying applications
- **Static file caching** - Optimized caching for images, CSS, JavaScript, etc.
- **Security** - Denies access to `.ht` files (Apache compatibility)
- **Logging** - Separate access and error logs for each domain

## Usage

```bash
python createVhost.py domain.com
```

Replace `domain.com` with your actual domain name. The script will:
1. Copy and rename the template to `/etc/nginx/sites-available/domain.com.conf`
2. Replace all `domain.com` placeholders with your domain
3. Create symlink in `/etc/nginx/sites-enabled/`
4. Create `/var/www/domain.com` directory
5. Set ownership to `nginx:nginx`
6. Create test `index.html` file
7. Validate and reload Nginx

## Requirements

- Linux system with Nginx installed
- Python 3.x
- `colored` library (install via `pip install colored`)
- Root or sudo privileges (required for system directories and Nginx operations)

## Notes

- The script must be run with sufficient privileges to access `/etc/nginx/` and `/var/www/`
- The template supports both HTTP and HTTPS configurations
- All status messages are color-coded for easy visual feedback
