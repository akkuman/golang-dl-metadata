# Golang Download Metadata Sync Automation

## 📋 Project Overview

This repository contains a GitHub Actions workflow for automatically synchronizing upstream metadata. The workflow runs daily to fetch the latest metadata from a specified upstream source and automatically commits updates to the repository.

## ⚙️ Features

- **Scheduled Automatic Sync**: Runs daily at 04:05 UTC
- **Manual Trigger Support**: Can be manually triggered via GitHub Actions interface
- **Automatic Commit**: Automatically commits and pushes when metadata changes are detected
- **Full History Tracking**: Fetches complete Git history for accurate change comparison

## 🚀 Quick Start

### Prerequisites

- GitHub account
- Write access to this repository (for automatic push functionality)

### Workflow Description

1. **Trigger Conditions**:

    - Scheduled: Daily at 04:05 UTC (adjustable via configuration file)
    - Manual: Click "Run workflow" in GitHub Actions page
2. **Execution Steps**:

    - Checkout repository code (with full Git history)
    - Download metadata from upstream source (`go.dev/dl/`)
    - Compare metadata changes
    - Automatically commit and push to repository if changes are detected

## 📁 File Structure

```markdown
.github/workflows/
└── sync.yml          # GitHub Actions workflow configuration
metadata.json         # Auto-generated metadata file (workflow output)
README.md            # This documentation
```

## 🔧 Configuration

### Environment Variables

- `UPSTREAM_METADATA`: Upstream metadata source URL

  - Default: `"go.dev/dl/?mode=json&include=all"`
  - Can be modified to sync from other data sources

### Scheduled Job Configuration

Currently configured to execute daily at 04:05 UTC. To modify, edit the cron expression in `.github/workflows/sync.yml`:

```yaml
schedule:
  - cron: '5 4 * * *'  # Format: minute hour day month day-of-week
```

### Manual Trigger

1. Navigate to the **Actions** tab in your GitHub repository
2. Select the **sync** workflow from the left sidebar
3. Click the **Run workflow** button
4. Select the branch and click the green run button

## 📄 Output Files

### metadata.json

- **Location**: Repository root directory
- **Content**: Latest metadata fetched from upstream source
- **Update Frequency**: Automatically updated daily, or on manual trigger
- **Format**: JSON format containing all version information from upstream

## 🔍 Monitoring & Troubleshooting

### Viewing Run History

1. Navigate to the **Actions** tab in your repository
2. Click on the **sync** workflow
3. Select a specific run to view detailed logs

### Common Issues

1. **Sync Failures**

    - Check network connectivity
    - Verify upstream URL is accessible
    - Review Actions logs for detailed error messages
2. **No Commits Made**

    - Workflow detects if metadata has actually changed
    - If upstream data hasn't been updated, no commit will be made
    - Log will show "No metadata changes to commit"
3. **Permission Issues**

    - Ensure GitHub Actions has write access to the repository
    - For organization repositories, check organization-level permissions

## 🤝 Contributing

To modify the workflow configuration:

1. Clone this repository
2. Modify the `.github/workflows/sync.yml`file
3. Commit changes and create a Pull Request
4. Merge to main branch after review

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details (if present)

## 📞 Support & Feedback

If you encounter issues or need assistance:

1. Check GitHub Actions run logs
2. Create an Issue describing the problem
3. Provide relevant error information and environment details

---

**Note**: This workflow will push changes directly to the main branch. Please ensure you understand the implications before deploying and using this workflow.