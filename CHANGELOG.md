# Google Recaptcha Changelog

## 3.1.0 - 2026-08-05

Merges upstream `juban/craft-google-recaptcha` up to 97e3fc3, which brings the v3 `formId` option and the
`getVersion`/`getSiteKey` Twig variables into this fork, then hardens the `formId` implementation.

### Added

- v3 `formId` option (from upstream), which mints the token on the form's `submit` event instead of on page load.
  Without it, a v3 token expires two minutes after the page loads and anyone slower than that is rejected with
  `timeout-or-duplicate`.
- New `getVersion` and `getSiteKey` Twig variables (from upstream).

### Fixed

- The `formId` script tag now receives `scriptOptions` attributes, so a CSP `nonce` is applied to it. Upstream's
  version omitted them, which meant the script was blocked under a strict CSP.
- The form is now submitted even when `grecaptcha.execute()` rejects or hangs (10s cap). Upstream's version left the
  promise unhandled, so a failed or slow reCAPTCHA call left the submit button permanently dead. Verification remains
  server-side, so this weakens nothing.
- A submit made before the reCAPTCHA API has initialised now waits for a token rather than posting an empty field.
- Repeated clicks while a token is in flight are ignored rather than firing several `execute()` calls.
- Interpolated values in the v3 `formId` script are JSON-encoded rather than pasted into bare JS string literals.

> {note} This fork's `3.0.0`–`3.0.6` tags are unrelated to upstream's `3.0.0`. The entry below is upstream's.

## 3.0.0 - 2024-11-06

### Added

- Craft 5 support
- v3 `formId` option in order to prevent `timeout-or-duplicate` errors if the form takes more than 2 minutes to be
  submitted (#8)
- New `getVersion` and `getSiteKey` Twig variables

## 2.3.0 - 2023-01-22

### Added

- `BeforeRecaptchaVerifyEvent` event to bypass or cancel the reCAPTCHA verification (original request by @creode-dev)

## 2.2.0 - 2022-08-15

### Added

- Ability to set script tags extra attributes (original request by @jcdarwin for CSP compliance)

## 2.1.0 - 2022-07-23

> {note} The plugin’s package name has changed to `jub/craft-google-recaptcha`. You can update the plugin by running
`composer require jub/craft-google-recaptcha && composer remove simplonprod/craft-google-recaptcha`.

### Changed

- Migrate plugin to `jub/craft-google-recaptcha`
- Updated plugin logo

## 2.0.2 - 2022-05-13

### Fixed

- Fix an exception that could occur in verify method if no actions parameters were saved (merged from 1.1.1)

## 2.0.1 - 2022-05-09

### Fixed

- reCAPTCHA v3 actions parameters were missing from the control panel

## 2.0.0 - 2022-05-08

### Added

- Added Craft 4 compatibility.

## 1.1.1 - 2022-05-13

### Fixed

- Fix an exception that could occur in verify method if no actions parameters were saved.

## 1.1.0 - 2022-03-07

### Added

- (v3 API) Default action name and score threshold can be configured
- (v3 API) Score threshold can be defined per action
- (v3 API) Ability to specify the action name in the twig `craft.googleRecaptcha.render()` function first parameter.

### Changed

- Google reCAPTCHA plugin options can now be set using environment variables
- Bump minimum required Craft version to 3.7.29

## 1.0.4 - 2021-05-03

### Added

- Contact form instructions in README

### Changed

- Updated plugin icon

## 1.0.3 - 2021-05-01

### Changed

- Update docs, issues and changelog links in composer.json
- Upgrade codeception to v4
- Fix composer dependencies
- Settings view refinements
- Various small refactoring

## 1.0.2 - 2021-04-20

### Added

- Full unit and functional tests coverage

### Changed

- Templates to render v2 and v3 tags
- More robust settings validation rules

## 1.0.1 - 2021-04-07

### Added

- instantRender parameter to twig render method (for v2 ajax calls context)

## 1.0.0 - 2021-04-01

### Added

- Initial release
