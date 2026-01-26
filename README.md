# Snyk Security Scanning Demo

This repository demonstrates automated security scanning using **Snyk** and **GitHub Actions**.

## 🎯 Purpose

This is a **training repository** that contains:
- ✅ Intentionally vulnerable Flask application (`app.py`)
- ✅ Automated security scanning workflows
- ✅ Multiple scan types: SAST, SCA, IaC, and Container scanning

**⚠️ WARNING**: This code contains deliberate security vulnerabilities for educational purposes. **DO NOT** use in production!

## 🔧 What's Inside

### Application Files
- **`app.py`**: Deliberately insecure Flask web application with common vulnerabilities
  - SQL Injection
  - Command Injection
  - Server-Side Template Injection (SSTI)
  - Insecure TLS
  - Insecure Deserialization
  - Hard-coded secrets

- **`requirements.txt`**: Python dependencies (some with known vulnerabilities)
- **`Dockerfile`**: Container configuration for Docker image scanning

### GitHub Actions Workflows

- **`.github/workflows/reusable_workflow.yaml`**: Reusable security scanning workflow
  - SCA (Software Composition Analysis) - scans dependencies
  - SAST (Static Application Security Testing) - scans code
  - IaC (Infrastructure as Code) - scans config files
  - Container scanning - scans Docker images

- **`.github/workflows/on_push.yaml`**: Triggers scans on push to main branch

## 🚀 Setup Instructions

### 1. Get a Snyk Account

1. Sign up at [snyk.io](https://snyk.io)
2. Get your **API Token**: Settings → General → Auth Token
3. Note your **Organization Slug**: Settings → General → Organization ID

### 2. Configure GitHub Secrets

1. Go to your repository: **Settings → Secrets and variables → Actions**
2. Click **"New repository secret"**
3. Add two secrets:
   - **Name**: `SNYK_TOKEN` → **Value**: Your Snyk API token
   - **Name**: `SNYK_ORG` → **Value**: Your Snyk organization slug

### 3. Enable GitHub Actions

1. Go to **Actions** tab in your repository
2. If prompted, click **"I understand my workflows, go ahead and enable them"**

## 📊 How It Works

### Automatic Scanning
Every time you push code to the `main` branch:
1. GitHub Actions triggers the workflow
2. Snyk SAST scan analyzes the code for vulnerabilities
3. Results are uploaded to Snyk dashboard
4. Build fails if high/critical issues are found
5. Report link appears in the Actions summary

### Current Configuration

The active workflow (`on_push.yaml`) runs:
- ✅ **SAST Scan** (Code Analysis)
- ❌ SCA Scan (disabled)
- ❌ Container Scan (disabled)
- ❌ IaC Scan (disabled)

### Enabling Other Scans

Edit `.github/workflows/on_push.yaml` to enable additional scans:

```yaml
jobs:
  # Uncomment to enable SCA scanning
  # sca_scan:
  #   uses: ./.github/workflows/reusable_workflow.yaml
  #   with:
  #     PROFILE: app
  #     SCA_scan: snyk
  #     SAST_scan: none
  #   secrets:
  #     SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
  #     Snyk_Org: ${{ secrets.SNYK_ORG }}

  # Uncomment to enable Container scanning
  # container_scan:
  #   uses: ./.github/workflows/reusable_workflow.yaml
  #   with:
  #     PROFILE: image_scan
  #     CONTAINER_scan: snyk
  #   secrets:
  #     SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
  #     Snyk_Org: ${{ secrets.SNYK_ORG }}
```

## 🔍 Expected Scan Results

When you run the scans, Snyk should detect:

### SAST (Code) Findings:
- Hard-coded API key
- SQL Injection vulnerability
- Command Injection vulnerability
- Server-Side Template Injection (SSTI)
- Insecure TLS configuration
- Insecure deserialization

### SCA (Dependencies) Findings:
- Known vulnerabilities in Flask 2.0.1
- Known vulnerabilities in requests 2.25.1
- Known vulnerabilities in urllib3 1.26.5

## 📚 Learning Resources

- [Snyk Documentation](https://docs.snyk.io/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)

## ⚠️ Security Notice

This repository is for **educational purposes only**. The code intentionally contains security vulnerabilities to demonstrate security scanning tools.

**Never**:
- Deploy this code to production
- Use these coding patterns in real applications
- Expose this application to the internet

## 📝 License

MIT License - See LICENSE file for details

---

**Happy Learning! 🎓**
# Test
