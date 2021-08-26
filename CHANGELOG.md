# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Add annotation which sets `ludacris` as app owner.
- Allow ingress on port 8000 for scraping metrics.
- Add ServiceMonitor for metrics to be scraped.
- Push `kyverno` to `giantswarm` catalog.

## [0.3.0] - 2021-07-09

### Added

- Add annotation to use `config-controller`.

### Changed

- \[CI/CD\] Push kyverno to app collections.
- Update Kyverno to `v1.4.1`.

## [0.2.0] - 2021-06-25

### Changed

- Disable default policies.

## [0.1.0] - 2021-06-24

### Changed

- Enable high availability (3 replicas).
- Update Kyverno to `1.4.0`.
- Reduce memory limit.

## [0.0.5] - 2021-06-03

### Changed

- Update Kyverno to `1.3.6`

## [0.0.4] - 2021-05-24

## [0.0.3] - 2021-03-24

## [0.0.2] - 2021-03-23

## [0.0.1] - 2021-03-19

[Unreleased]: https://github.com/giantswarm/kyverno-app/compare/v0.3.0...HEAD
[0.3.0]: https://github.com/giantswarm/kyverno-app/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/giantswarm/kyverno-app/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/giantswarm/kyverno-app/compare/v0.0.5...v0.1.0
[0.0.5]: https://github.com/giantswarm/kyverno-app/compare/v0.0.4...v0.0.5
[0.0.4]: https://github.com/giantswarm/kyverno-app/compare/v0.0.3...v0.0.4
[0.0.3]: https://github.com/giantswarm/kyverno-app/compare/v0.0.2...v0.0.3
[0.0.2]: https://github.com/giantswarm/kyverno-app/compare/v0.0.1...v0.0.2
[0.0.1]: https://github.com/giantswarm/kyverno-app/releases/tag/v0.0.1
