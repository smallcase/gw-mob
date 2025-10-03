# React Native Production Release Guide

This document explains how to create production releases for the React Native mobile application.

## Standard Operating Procedure (S.O.P.)

### Phase 1: Branch Setup & Native Integration

1. **Checkout from dev branch**

   ```bash
   git checkout dev
   git pull origin dev
   git checkout -b release/v{major}.{minor}.{patch}
   ```

2. **Apply Native Changes**
   - Update native iOS/Android dependencies if needed
   - Sync native module versions
   - Commit all changes

### Phase 2: Version Bump & Changelog

3. **Run Release Command**

   ```bash
   yarn release:patch   # Bug fixes (x.x.X)
   yarn release:minor   # New features (x.X.0)
   yarn release:major   # Breaking changes (X.0.0)
   yarn release:major:rc # Release candidate (X.0.0-rc.N)
   ```

   This automatically:

   - Bumps version in `package.json`
   - Creates git commit and tag

### Phase 3: Push & Create PR

5. **Push with Tags**

   ```bash
   git push origin release/v{major}.{minor}.{patch}
   git push origin --tags
   ```

6. **Create PR to prod**
   - Create PR from `release/v{version}` → `prod`
   - Wait for all bitrise/code review workflows to complete

### Phase 4: Merge

7. **Merge to prod**
   - Ensure all checks pass
   - Merge PR
   - Wait for merge workflow to complete

### Phase 5: Publish

8. **Publish to NPM**
   - Go to **Github Actions** tab
   - Select **Publish to NPM** workflow
   - Click **Run workflow**
   - Select `prod` branch
   - Click **Run workflow**
