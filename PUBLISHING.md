# Publishing to PyPI

This guide explains how to publish `copilotkit-langgraph-history` to PyPI.

## Prerequisites

1. **PyPI account**: Create at https://pypi.org/account/register/
2. **Email verified**: Check your email and verify your PyPI account
3. **Build tools installed**: Already done ✓

## Quick Start

### Method 1: Manual Publishing

```bash
cd python/

# 1. Build the package
python3 -m build

# 2. Upload to PyPI
python3 -m twine upload dist/*
```

When prompted:
- **Username**: `__token__`
- **Password**: Your PyPI API token (starts with `pypi-`)

### Method 2: Using API Token in Config

Save your token once:

```bash
# Create/edit ~/.pypirc
cat > ~/.pypirc << EOF
[pypi]
username = __token__
password = pypi-YOUR_TOKEN_HERE
EOF

chmod 600 ~/.pypirc
```

Then publish:

```bash
python3 -m twine upload dist/*
```

## Creating a PyPI API Token

1. Go to: https://pypi.org/manage/account/token/
2. Click "Add API token"
3. **Token name**: `copilotkit-langgraph-history`
4. **Scope**: 
   - First publish: "Entire account"
   - After first publish: "Project: copilotkit-langgraph-history" (more secure)
5. Click "Add token"
6. **Copy the token immediately!**

## Version Bumping

Update version in `pyproject.toml`:

```toml
[project]
version = "0.1.1"  # Bump this
```

### Semantic Versioning

- **Patch** (0.1.0 → 0.1.1): Bug fixes
- **Minor** (0.1.0 → 0.2.0): New features, backward compatible
- **Major** (0.1.0 → 1.0.0): Breaking changes

## Publishing Workflow

```bash
# 1. Update version in pyproject.toml
# Edit: version = "0.1.1"

# 2. Clean previous builds
rm -rf dist/ build/ *.egg-info

# 3. Build new version
python3 -m build

# 4. Check the build
python3 -m twine check dist/*

# 5. Upload to PyPI
python3 -m twine upload dist/*

# 6. Verify it's live
pip install copilotkit-langgraph-history --upgrade
```

## Testing Before Publishing (TestPyPI)

Use TestPyPI to test your package before publishing to the real PyPI:

```bash
# 1. Create TestPyPI account: https://test.pypi.org/account/register/

# 2. Get TestPyPI token: https://test.pypi.org/manage/account/token/

# 3. Upload to TestPyPI
python3 -m twine upload --repository testpypi dist/*

# 4. Test installation
pip install --index-url https://test.pypi.org/simple/ copilotkit-langgraph-history

# 5. If all works, publish to real PyPI
python3 -m twine upload dist/*
```

## Troubleshooting

### "Package already exists"

If you get a 403 error saying the package exists:
- The package name is taken
- Or you need to bump the version number (can't republish same version)

### "Invalid credentials"

- Make sure username is exactly `__token__` (with underscores)
- Check your token hasn't expired
- Generate a new token

### "File already exists"

You're trying to upload a version that's already on PyPI. Bump the version in `pyproject.toml`.

## After Publishing

1. **Verify on PyPI**: https://pypi.org/project/copilotkit-langgraph-history/
2. **Test installation**:
   ```bash
   pip install copilotkit-langgraph-history
   ```
3. **Update README** if needed
4. **Create GitHub release** with the same version tag

## Package URLs

After publishing:
- **PyPI**: https://pypi.org/project/copilotkit-langgraph-history/
- **Documentation**: Your GitHub README
- **Repository**: https://github.com/alakaybenjamin/copilotkit-langgraph-history-python

## Automated Publishing (GitHub Actions)

Want to automate publishing? Add this workflow to `.github/workflows/publish.yml`:

```yaml
name: Publish Python Package

on:
  release:
    types: [published]

jobs:
  pypi-publish:
    name: Upload to PyPI
    runs-on: ubuntu-latest
    permissions:
      id-token: write
    steps:
      - uses: actions/checkout@v4
      
      - uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      
      - name: Install build tools
        run: python -m pip install --upgrade build
      
      - name: Build package
        run: python -m build
      
      - name: Publish to PyPI
        uses: pypa/gh-action-pypi-publish@release/v1
        with:
          password: ${{ secrets.PYPI_API_TOKEN }}
```

Then add your `PYPI_API_TOKEN` to GitHub Secrets.

## Related

- [PyPI Help](https://pypi.org/help/)
- [Python Packaging Guide](https://packaging.python.org/)
- [Twine Documentation](https://twine.readthedocs.io/)
