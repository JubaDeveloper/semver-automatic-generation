# Semantic Versioning Pattern

This repository implements an automatic semantic versioning pattern using GitHub Actions and semantic-release.

## Commit Message Pattern

This project uses a strict commit message pattern to automatically generate semantic versions:

### Basic Pattern
```
type(scope): description
```

### Supported Types

#### Versioning Types
- **`major(...): ...`** - Creates a major version bump (breaking changes)
- **`minor(...): ...`** - Creates a minor version bump (new features)
- **`patch(...): ...`** - Creates a patch version bump (bug fixes)

#### Standard Types (following conventional commits)
- **`feat(...): ...`** - New feature (minor version)
- **`fix(...): ...`** - Bug fix (patch version)
- **`perf(...): ...`** - Performance improvement (patch version)
- **`revert(...): ...`** - Revert previous changes (patch version)

#### Non-versioning Types
- **`docs(...): ...`** - Documentation changes (no version)
- **`style(...): ...`** - Code style changes (no version)
- **`chore(...): ...`** - Maintenance tasks (no version)
- **`refactor(...): ...`** - Code refactoring (no version)
- **`test(...): ...`** - Adding/updating tests (no version)
- **`build(...): ...`** - Build system changes (no version)
- **`ci(...): ...`** - CI/CD changes (no version)

### Environment-Specific Pattern
You can also target specific environments:

```
type(scope)[environment]: description
```

Examples:
- `patch(api)[prod]: fix critical security issue`
- `minor(ui)[staging]: add new dashboard features`
- `major(core)[dev]: restructure database schema`

## Examples

```bash
# Major version bump (1.0.0 -> 2.0.0)
git commit -m "major(api): breaking change in authentication system"

# Minor version bump (1.0.0 -> 1.1.0)
git commit -m "minor(ui): add user profile page"
git commit -m "feat(auth): implement OAuth2 login"

# Patch version bump (1.0.0 -> 1.0.1)
git commit -m "patch(db): fix connection timeout issue"
git commit -m "fix(validation): correct email regex pattern"

# No version change
git commit -m "docs(readme): update installation instructions"
git commit -m "chore(deps): update dependencies"

# Environment-specific releases
git commit -m "patch(security)[prod]: fix XSS vulnerability"
git commit -m "minor(features)[staging]: add beta feature toggles"
```

## How It Works

1. **Commit Analysis**: When code is pushed to `main` or `master`, the GitHub Action analyzes commit messages
2. **Version Calculation**: Based on commit types, it determines the next semantic version
3. **Release Creation**: Automatically creates a GitHub release with generated changelog
4. **Tagging**: Creates a Git tag with the new version number

## Files

- `.github/actions/generate_semver/action.yaml` - Custom GitHub Action for semantic versioning
- `.github/workflows/generate_semver.yaml` - Workflow that runs the action
- `.releaserc.json` - Semantic-release configuration (auto-generated)

## Setup

1. Ensure your repository has a `main` or `master` branch
2. Make sure GitHub Actions are enabled
3. Commit using the specified patterns
4. Push to the main branch to trigger automatic versioning

## Validation

The workflow includes commit message validation for pull requests, ensuring all commits follow the required pattern before merging.