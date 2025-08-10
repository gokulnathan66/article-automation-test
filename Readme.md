# Article Automation Test Repository

🧪 **Test repository demonstrating the multi-platform blog publishing system**

This repository serves as a **demonstration and testing ground** for the [article-automation](https://github.com/gokulnathan66/article-automation) GitHub Actions that automatically publish content to Hashnode and Dev.to.

## 🎯 Purpose

This repository demonstrates:
- ✅ How to structure content for automated publishing
- ✅ Proper workflow configuration
- ✅ Integration with multiple blogging platforms
- ✅ Automated image URL conversion
- ✅ Post update functionality

## 📁 Repository Structure

article-automation-test/
├── content/
│ └── README.md # Test article content
├── images/ # Referenced images (optional)
│ └── demo-screenshot.png
├── .github/workflows/
│ └── publish.yml # Publishing workflow
└── README.md # This file
text

## 📝 Test Content

The test article in `content/README.md` includes:

- **Title extraction** from `# heading`
- **Markdown formatting** examples
- **Image references** (converted to GitHub raw URLs automatically)
- **Tag specification** at the end
- **Various content types** to test parsing

## 🔄 How It Works

When content is pushed to the `main` branch:

1. **GitHub Actions Trigger**: The workflow in `.github/workflows/publish.yml` runs
2. **Content Processing**: Actions read `content/README.md`
3. **Image URL Conversion**: Relative image paths → GitHub raw URLs
4. **Multi-Platform Publishing**:
   - **Hashnode**: Uses GraphQL API to publish/update
   - **Dev.to**: Uses REST API to publish/update
5. **State Management**: Saves post IDs for future updates

## ⚙️ Workflow Configuration

.github/workflows/publish.yml
name: Multi-Platform Publishing
on:
push:
branches: [main]
workflow_dispatch: # Manual trigger option
jobs:
publish-hashnode:
runs-on: ubuntu-latest
steps:
- name: Checkout content
uses: actions/checkout@v4
text
  - name: Publish to Hashnode
    uses: gokulnathan66/article-automation/hashnode-publish@main
    with:
      hashnode-pat: ${{ secrets.HASHNODE_PAT }}
      hashnode-publication-id: ${{ secrets.HASHNODE_PUBLICATION_ID }}
      hashnode-publication-host: ${{ secrets.HASHNODE_PUBLICATION_HOST }}
      github-token: ${{ secrets.VAR_EDIT_TOKEN_GIT }}
      # Post state management
      saved-post-id: ${{ vars.HASHNODE_SAVED_POST_ID }}
      saved-post-slug: ${{ vars.HASHNODE_SAVED_POST_SLUG }}
      saved-post-title: ${{ vars.HASHNODE_SAVED_POST_TITLE }}
      saved-post-url: ${{ vars.HASHNODE_SAVED_POST_URL }}
      saved-post-published-at: ${{ vars.HASHNODE_SAVED_POST_PUBLISHED_AT }}
      saved-post-updated-at: ${{ vars.HASHNODE_SAVED_POST_UPDATED_AT }}
publish-devto:
runs-on: ubuntu-latest
steps:
- name: Checkout content
uses: actions/checkout@v4
text
  - name: Publish to Dev.to
    uses: gokulnathan66/article-automation/devto-publish@main
    with:
      devto-api-key: ${{ secrets.DEV_TO_API_KEY }}
      github-token: ${{ secrets.VAR_EDIT_TOKEN_GIT }}
      # Post state management
      saved-post-id: ${{ vars.DEV_TO_SAVED_POST_ID }}
      saved-post-title: ${{ vars.DEV_TO_SAVED_POST_TITLE }}
      saved-post-url: ${{ vars.DEV_TO_SAVED_POST_URL }}
      saved-post-published-at: ${{ vars.DEV_TO_SAVED_POST_PUBLISHED_AT }}
      saved-post-updated-at: ${{ vars.DEV_TO_SAVED_POST_UPDATED_AT }}
text

## 🔐 Required Secrets

This test repository requires these secrets to be configured:

### Repository Settings → Secrets and variables → Actions:

**For Hashnode Integration:**
- `HASHNODE_PAT` - Personal Access Token from Hashnode
- `HASHNODE_PUBLICATION_ID` - Your publication ID  
- `HASHNODE_PUBLICATION_HOST` - Publication domain (e.g., `test.hashnode.dev`)

**For Dev.to Integration:**
- `DEV_TO_API_KEY` - API key from Dev.to

**For Both Platforms:**
- `VAR_EDIT_TOKEN_GIT` - GitHub token with `repo` and `actions:write` scopes

## 🎮 Testing the System

### Option 1: Manual Trigger
1. Go to **Actions** tab in this repository
2. Select **"Multi-Platform Publishing"** workflow
3. Click **"Run workflow"**
4. Watch the execution in real-time

### Option 2: Content Update
1. Edit `content/README.md`
2. Commit and push to `main` branch
3. Workflow triggers automatically
4. Check the Actions tab for execution logs

### Option 3: Fork and Test
1. Fork this repository
2. Configure your own secrets
3. Update `content/README.md` with your content
4. Push changes to see it published to your platforms

## 📊 What Happens During Execution

### **Phase 1: Setup**
- ✅ Checkout action repository
- ✅ Setup Node.js environment
- ✅ Install dependencies

### **Phase 2: Content Processing**
- 🔍 Locate README.md file
- 📝 Extract title from first `# heading`
- 🖼️ Convert relative image URLs to GitHub raw URLs
- 🏷️ Parse tags from `Tags:` line

### **Phase 3: Platform Publishing**
- **Hashnode**: GraphQL API calls for publish/update
- **Dev.to**: REST API calls for publish/update
- 🔍 Check for existing posts by title
- ✅ Create new or update existing post

### **Phase 4: State Management**
- 💾 Save post IDs to repository variables
- 📊 Store metadata for future updates
- ✅ Enable smart update functionality

## 🔧 Debugging

### Check Execution Logs:
1. Go to **Actions** tab
2. Click on the latest workflow run
3. Expand job steps to see detailed logs
4. Look for error messages or debug information

### Common Test Scenarios:
- **First Run**: Creates new posts on both platforms
- **Content Update**: Updates existing posts
- **Image Processing**: Verifies URL conversion works
- **Tag Handling**: Tests tag parsing and application

## 📈 Expected Results

After successful execution:

1. **Hashnode**: Article published/updated at your publication
2. **Dev.to**: Article published/updated on your Dev.to profile
3. **Repository Variables**: Post metadata saved for future updates
4. **Images**: All relative paths converted to accessible GitHub URLs

## 🎯 Use This Repository To:

- ✅ **Learn**: Understand how the automation works
- ✅ **Test**: Verify setup before using in production
- ✅ **Debug**: Troubleshoot configuration issues
- ✅ **Fork**: Create your own automated blog publishing system

## 🔗 Related Links

- 🏠 **Main Action Repository**: [article-automation](https://github.com/gokulnathan66/article-automation)
- 📚 **Hashnode**: [hashnode.com](https://hashnode.com)
- 📝 **Dev.to**: [dev.to](https://dev.to)
- 🔧 **GitHub Actions**: [GitHub Actions Documentation](https://docs.github.com/en/actions)

## 🤝 Contributing

Found issues or have improvements? 
1. Create an issue in the [main repository](https://github.com/gokulnathan66/article-automation/issues)
2. Submit a pull request with your changes
3. Share your testing results and feedback

---

**This is a test repository for the article automation system. For the actual actions, see [article-automation](https://github.com/gokulnathan66/article-automation).**