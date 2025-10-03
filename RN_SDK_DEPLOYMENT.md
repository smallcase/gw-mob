# React Native Release Guide

## Release Types

### Internal Releases

Internal releases are for QA/testing after updating dependencies. These are manual builds distributed internally.

### Production Releases

Production releases are published to NPM registry following the full S.O.P. workflow.

---

## Internal Release (APK / IPA Generation)

Use this for generating **internal builds** for QA/testing after updating dependencies.

### 1. Generate Android Release APK

```bash
yarn generateAndroidRelease
```

Or manually:

```bash
cd android && ./gradlew assembleRelease
```

**Output location:** `android/app/build/outputs/apk/release/app-release.apk`

### 2. Generate iOS Release IPA

**Steps in Xcode:**

1. Open the project workspace: `ios/{AppName}.xcworkspace`
2. Archive the app
3. Export IPA using Ad Hoc or Development distribution
4. Save the `.ipa` file locally

**Output location:** Selected export path (Archives stored at `~/Library/Developer/Xcode/Archives/`)

### 3. Distribute Internally

- Share APK/IPA via Slack/Firebase App Distribution, Drive, or MDM tool
- Notify QA team for testing

---

## Production Release S.O.P.

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
   - Generates/updates `CHANGELOG.md`
   - Creates git commit and tag

4. **Review Changes**
   ```bash
   git log -1 --stat
   git show HEAD
   ```

### Phase 3: Push & Create PR

5. **Push with Tags**

   ```bash
   git push origin release/v{major}.{minor}.{patch}
   git push origin --tags
   ```

6. **Create PR to prod**
   - Create PR from `release/v{version}` → `prod`
   - Wait for all workflows to complete

### Phase 4: Merge

7. **Merge to prod**
   - Ensure all checks pass
   - Merge PR
   - Wait for merge workflow to complete
   - Delete release branch

### Phase 5: Publish

8. **Publish to NPM**

   - Go to **Actions** tab
   - Select **Publish to NPM** workflow
   - Click **Run workflow**
   - Select `prod` branch
   - Click **Run workflow**

9. **Post-Release**
   - Verify NPM publication
   - Create GitHub Release
   - Create backmerge PR from `prod` → `dev`
