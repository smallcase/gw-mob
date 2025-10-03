# Flutter Release Guide

## Release Types

### Internal Releases

Internal releases are for QA/testing after updating dependencies. These are manual builds distributed internally.

### Production Releases

Production releases are published to Pub.dev following the full S.O.P. workflow.

---

## Internal Release (APK / IPA Generation)

⚡ Use this for generating **internal builds** for QA/testing.

### 1. Generate Android Release APK

```bash
flutter build apk --release
```

**Output location:** `build/app/outputs/flutter-apk/app-release.apk`

### 2. Generate iOS Release IPA

```bash
flutter build ipa --release
```

**Output location:** `build/ios/ipa/`

### 3. Distribute Internally

- Share APK/IPA via Slack, Drive, or MDM tool
- Notify QA team for testing

---

## Production Release S.O.P.

### Phase 1: Setup & Version Update

1. **Checkout from master**

   ```bash
   git checkout master
   git pull origin master
   git checkout -b release/v{major}.{minor}.{patch}
   ```

2. **Apply Changes**
   - Update native dependencies if needed
   - Manually update version in `pubspec.yaml`
   - Commit changes

### Phase 2: PR & Verification

3. **Create PR to master**

   ```bash
   git push origin release/v{version}
   ```

   - Create PR from `release/v{version}` → `master`
   - Verify release branch is working fine
   - Wait for workflows to complete

4. **Merge to master**
   - Merge PR after all checks pass

### Phase 3: Local Testing

5. **Pull & Test**
   ```bash
   git checkout master
   git pull origin master
   flutter run --release
   ```
   - Check console for errors/warnings

### Phase 4: Publish (Authorized Personnel Only)

6. **Dry Run**

   ```bash
   flutter pub publish --dry-run
   ```

7. **Publish to Pub.dev**

   ```bash
   flutter pub publish
   ```

8. **Post-Release**
   - Verify package on pub.dev
