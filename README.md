# exponential-php-floor

A Composer metapackage that lets **Exponential 6.0.15 and later** install on every PHP
version it runs on, with Composer's security blocking left on.

> **Supported: PHP 8.0 to 8.5. Usable without support: PHP 7.4 (Exponential 6.0.15 and later).**
> On PHP 7.4 the software is designed to be usable, but there is no bug-fix or security commitment
> specific to PHP 7.4 (use it at your own risk), and the features that need PHP 8 are not available.

Exponential's kernel is usable on PHP 7.4, without support. Some of the extensions it installs by default, and some
of the libraries they use, need a newer PHP. Instead of one fixed list that only fits the
newest PHP, the kernel requires this metapackage, and each version of the metapackage
belongs to one PHP range. Composer picks the version whose PHP range matches the PHP it runs
on, and with it the set of extension releases that run there. Nobody has to choose anything
by hand.

```json
"require": {
    "se7enxweb/exponential-php-floor": "^1.0"
}
```

## Versions

| Version | PHP           | What it requires |
|---------|---------------|------------------|
| 1.0.0   | 7.4 (without support) | Superseded by 1.0.1: it also required sevenx_dse ~1.1.14 and xrowextract ~2.5.18, whose code does not run on PHP 7.4 (the 7.4 boot check found it after the release). |
| 1.0.1   | 7.4 (without support) | The last PHP 7.4 releases of the lines that moved to PHP 8.0 a few days later: bccie ~1.1.18, cjw_newsletter ~4.2.14, eztags ~2.4.23, git_manager ~2.0.22, syndication ~1.3.10, and google/recaptcha ~1.2.4 (the 1.x line that still runs on PHP 7.4). xrowextract and sevenx_dse are left out on PHP 7.4. |
| 1.0.2   | 7.4 (without support) | The set of 1.0.1, plus ezodf ~7.0.4 (Exponential activates ezodf; without it a PHP 7.4 installation logged "Extension 'ezodf' does not exist"), and eztags ~2.4.31. Both releases install on PHP 7.4 again. |
| 1.1.0   | 8.0           | The extensions that need PHP 8.0, at the versions the kernel asks for: Exponential Velocity, two-factor authentication, sqliimport, expqueue, ezodf, exp_adminui, expai, the CJW theme packages and the rest, and google/recaptcha ~1.3.1. Not the Layouts family, which needs PHP 8.1. |
| 1.2.0   | 8.1 to 8.3    | Everything of 1.1.0, plus the Netgen Layouts port (explayouts and its packages), the expsite packages and the media site theme (sevenx-themes-media). google/recaptcha ~1.3.1, because 1.4 and later need PHP 8.4. |
| 1.3.0   | 8.4 and later | The same set as 1.2.0 with no limit on google/recaptcha, so the current 2.x line is installed. PHP 8.5 included. |
| 1.1.1   | 8.0           | The set of 1.1.0 at the extension releases of 29 October 2026, the ones the kernel required itself before it required this metapackage (Exponential Velocity ~0.0.4.57, eztags ~2.4.29, cjw_newsletter ~4.2.19, exp_adminui ~1.0.0.54 ...). 1.1.0 allowed older releases. |
| 1.2.1   | 8.1 to 8.3    | The set of 1.2.0 at the same releases as 1.1.1, plus explayouts ~1.4.46, explayouts-ui ~1.3.31, explayouts-ui-api ~1.3.34 and sevenx-themes-media ~1.5.80. |
| 1.3.1   | 8.4 and later | The set of 1.3.0 at the same releases as 1.2.1. |
| 1.1.2, 1.2.2, 1.3.2 | 8.0; 8.1 to 8.3; 8.4 and later | The sets of 1.1.1, 1.2.1 and 1.3.1 with exp_adminui ~1.0.0.55 (the release whose footer links Exponential to exponential.earth), as the kernel requires since 29 October 2026. |

The numbers are chosen to read in PHP order: a higher minor version always means a higher
PHP floor. Composer installs the highest version whose `php` requirement the running PHP meets
(1.0.2 rather than 1.0.1 or 1.0.0 on PHP 7.4). The kernel names the lowest patch release of each line it
accepts, `~1.0.2 || ~1.1.2 || ~1.2.2 || ~1.3.2`, so a version that would allow older extension
releases than the kernel asks for (1.0.0, 1.0.1, 1.1.0, 1.1.1, 1.2.0, 1.2.1, 1.3.0, 1.3.1) is never installed.

## What is not available on PHP 7.4

On PHP 7.4 Composer leaves out what cannot run there, and the kernel says so instead of failing:

- **Exponential Velocity** (the application server) needs PHP 8.0. `exp:velocity start`
  refuses with a message on 7.4; Apache or nginx with PHP-FPM, and the built-in `php`
  engine, work as before.
- **Netgen Layouts** (explayouts), the expsite packages and the media site theme need PHP 8.1.
- Two-factor authentication, sqliimport 2.x, expqueue, exp_adminui,
  exp_enhanced_link, expai, expchangeclass, ezownerchange 1.4 and the CJW theme packages
  declare PHP 8.0 and are not installed on PHP 7.4. xrowextract and sevenx_dse do not run on
  PHP 7.4 and are left out by 1.0.1 and later. ezodf is installed on PHP 7.4 from 1.0.2 (ezodf 7.0.4).

## Maintaining it

- Every version is a git tag and a GitHub release. **A published tag is permanent**: it is
  never moved, deleted or re-cut. A mistake is fixed by the next version.
- When an extension publishes a release that runs on an older PHP again, the version for
  that range gets a new patch release (for example 1.0.1) that requires it.
- When the kernel's own requirements change, the version for each range is released again
  with the same rules.
- Check what is already published before choosing a number:
  `git tag -l --sort=version:refname` and `gh release list`.

## License

GNU General Public License v2.0 (or any later version), like Exponential.
