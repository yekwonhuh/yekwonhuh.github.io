# Ye Kwon Huh's personal website

One-page Jekyll site for https://yekwonhuh.github.io/. Publication is gated by S07 acceptance and S08 release approval; the manual deployment workflow remains local until S08 release approval.

## Local runtime

Pinned versions: Ruby 3.4.11, Bundler 2.6.9, Jekyll 4.4.1. The project-local runtime is under `.runtime/ruby`, with OpenSSL 3.5.9 under `.runtime/openssl` and libyaml 0.2.5 under `.runtime/libyaml`. Source archives and build logs are in `.runtime/build`; these directories are ignored. No system Ruby or shell profile changes are required. `.runtime` is not distributed in Git. On another machine, install Ruby 3.4.11 with YAML/OpenSSL support, and invoke `bundle install` / `bundle exec jekyll serve` using that runtime directly; the `scripts/with-ruby` commands below select this checkout’s local installation. Install Bundler with `gem install bundler -v 2.6.9 --no-document`.

## Preview and build

From this repository:

```sh
scripts/with-ruby bundle install
scripts/with-ruby bundle exec jekyll serve --host 127.0.0.1
```

Open http://127.0.0.1:4000/. Stop the preview with Ctrl-C. Production build:

```sh
JEKYLL_ENV=production scripts/with-ruby bundle exec jekyll build
```

Output is `_site/`. Never edit generated files. Gemfile.lock fixes the resolved gem versions; use Bundler 2.6.9 when updating dependencies. Changes to runtime pins require a new review.

## Edit content

- Prose: `_includes/content/about.md`, `expertise.md`, `research.md`, `education.md`, `updates.md`, `teaching-service.md`.
- Roles: `_data/experience.yml`; preserve the approved date labels.
- Profile and links: `_data/profile.yml`.
- Publications: `_data/publications.yml`; append an entry with a unique `id`, exact `title`, ordered `authors`, `venue`, numeric `year`, `status` (`published` or `under review`), and `url` (a verified link or `null`). Use optional `display_title` for a consistent sentence-case display while preserving original publisher wording/capitalization in `title`. Entries display by year descending within each status group; equal-year entries retain file order. The owner's name is automatically bolded.
- Visual styling: `assets/css/main.css`; markup: `_layouts/default.html`.

CV is currently non-clickable “CV (update coming)”. Its replacement requires the deferred S09 approval. Plans, specs, reviews, scripts, dependencies and historical review screenshots are excluded from public output.

## Release and rollback

Do not push or deploy until the exact S08 release is approved. The workflow `.github/workflows/pages.yml` only runs manually: select the approved branch and enter the approved full commit SHA as `release_sha`. It rejects a SHA that differs from the workflow-run commit. Configure repository Pages source as GitHub Actions before running. Ordinary pushes do not deploy. At launch, record the release commit and preserve the last accepted release. To roll back after approval, revert the unwanted change in Git, build and check the restored content, then publish that reviewed revert through the approved deployment process. Keep the Google Site available. The first-release deployment and migration-notice details are still gated in S08.
