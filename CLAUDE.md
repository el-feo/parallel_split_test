# Claude Code Guidelines for parallel_split_test

## Repository Structure

This is a fork of `grosser/parallel_split_test`. When working with PRs:
- **Always target `el-feo/parallel_split_test`** (this fork), not the upstream repo
- Use `--repo el-feo/parallel_split_test` explicitly with `gh pr create`
- Ask before interacting with the upstream `grosser` repo

## Version Constraints

- **"Support version X" ≠ "Require version X"** - Adding support for a new Ruby version should not drop support for older versions unless explicitly requested
- When updating `required_ruby_version`, prefer the broadest compatible range
- Clarify requirements before changing version constraints

## CI and Bundler Compatibility

- **Bundler 4 requires Ruby 3.2+** - If CI tests multiple Ruby versions including < 3.2, the `BUNDLED WITH` section in Gemfile.lock will cause failures
- Strip `BUNDLED WITH` from Gemfile.lock in CI for older Ruby versions:
  ```ruby
  ruby -e "File.write('Gemfile.lock', File.read('Gemfile.lock').split('BUNDLED WITH').first)"
  ```
- Test CI workflows against the **oldest supported Ruby version first** to catch compatibility issues early

## Testing

Run tests locally before pushing:
```bash
bundle exec rspec spec/
```

Test with specific Ruby version:
```bash
ASDF_RUBY_VERSION=3.3.10 bundle exec rspec spec/
```
