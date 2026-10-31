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
| 1.1.0   | 8.0           | The extensions that need PHP 8.0, at the versions the kernel asks for: Exponential Velocity, two-factor authentication, sqliimport, expqueue, ezodf, exp_adminui, expai, the CJW theme packages and the rest, and google/recaptcha ~1.3.1. It left out Exponential Layouts, the expsite packages and the media site theme, which run on PHP 8.0; 1.1.4 corrects that. |
| 1.2.0   | 8.1 to 8.3    | Everything of 1.1.0, plus Exponential Layouts (explayouts and its packages), the expsite packages and the media site theme (sevenx-themes-media). google/recaptcha ~1.3.1, because 1.4 and later need PHP 8.4. |
| 1.3.0   | 8.4 and later | The same set as 1.2.0 with no limit on google/recaptcha, so the current 2.x line is installed. PHP 8.5 included. |
| 1.1.1   | 8.0           | The set of 1.1.0 at the extension releases of 29 October 2026, the ones the kernel required itself before it required this metapackage (Exponential Velocity ~0.0.4.57, eztags ~2.4.29, cjw_newsletter ~4.2.19, exp_adminui ~1.0.0.54 ...). 1.1.0 allowed older releases. |
| 1.2.1   | 8.1 to 8.3    | The set of 1.2.0 at the same releases as 1.1.1, plus explayouts ~1.4.46, explayouts-ui ~1.3.31, explayouts-ui-api ~1.3.34 and sevenx-themes-media ~1.5.80. |
| 1.3.1   | 8.4 and later | The set of 1.3.0 at the same releases as 1.2.1. |
| 1.1.2, 1.2.2, 1.3.2 | 8.0; 8.1 to 8.3; 8.4 and later | The sets of 1.1.1, 1.2.1 and 1.3.1 with exp_adminui ~1.0.0.55 (the release whose footer links Exponential to exponential.earth), as the kernel requires since 29 October 2026. |
| 1.0.3   | 7.4 (without support) | The set of 1.0.2, plus Twig for the kernel's Twig template engine: se7enxweb/twig ~3.11.4, which runs on PHP 7.4. |
| 1.1.3   | 8.0           | The set of 1.1.2, plus se7enxweb/twig ~3.19.1, which runs on PHP 8.0. |
| 1.2.3, 1.3.3 | 8.1 to 8.3; 8.4 and later | The sets of 1.2.2 and 1.3.2, plus twig/twig ^3.27, the upstream releases that no security advisory affects. |
| 1.1.4   | 8.0           | The set of 1.1.3, plus Exponential Layouts (explayouts and its eleven packages), expquery-translator, the five expsite packages and the media site theme (sevenx-themes-media), at the releases 1.2.3 requires. Exponential supports PHP 8.0 with all of its extensions; 1.1.0 to 1.1.3 left these 19 packages out although they run on PHP 8.0. |
| 1.0.4, 1.1.5, 1.2.4, 1.3.4 | 7.4 (without support); 8.0; 8.1 to 8.3; 8.4 and later | The same packages as 1.0.3, 1.1.4, 1.2.3 and 1.3.3. Those tags were made before this README was corrected and still show its old text (that Layouts needed PHP 8.1); these versions carry the corrected README. |
| 1.2.5, 1.3.5 | 8.1 to 8.3; 8.4 and later | The sets of 1.2.4 and 1.3.4 with `twig/twig` `^3.27 \|\| ~3.19.1`: a platform that pins se7enxweb/twig 3.19.1 on every PHP version (Exponential Platform Legacy 3.x, and 4.6.x on PHP 8.4 and later) installs the kernel's current code again. 1.2.3, 1.2.4, 1.3.3 and 1.3.4 required `twig/twig` `^3.27` only, which se7enxweb/twig 3.19.1 cannot meet, so Composer fell back to the kernel release v6.0.14 on PHP 8.1 to 8.3 and found nothing on 8.4 and later. On its own the floor still installs `twig/twig` 3.27 or later. 1.0.x and 1.1.x needed no change. |

The numbers are chosen to read in PHP order: a higher minor version always means a higher
PHP floor. Composer installs the highest version whose `php` requirement the running PHP meets
(1.0.3 rather than 1.0.2, 1.0.1 or 1.0.0 on PHP 7.4). The kernel names the lowest patch release of each line it
accepts, `~1.0.3 || ~1.1.4 || ~1.2.3 || ~1.3.3`, so a version that would allow older extension
releases than the kernel asks for, or leave out Twig (1.0.0 to 1.0.2, 1.1.0 to 1.1.2, 1.2.0 to 1.2.2, 1.3.0 to 1.3.2), or leave out Exponential Layouts on PHP 8.0 (1.1.0 to 1.1.3), is never installed.

### Twig

Since 1.0.3, 1.1.3, 1.2.3 and 1.3.3 the metapackage, not the kernel, requires Twig, because no
single Twig requirement installs on every PHP version with Composer's security blocking on:
upstream twig/twig up to 3.26 is affected by security advisories, and 3.27 and later need PHP 8.1.
On PHP 8.1 and later the metapackage requires twig/twig ^3.27. On PHP 7.4 and 8.0 it requires
se7enxweb/twig, the maintained Twig 3 line for those PHP versions, which provides the same
`Twig\` classes. The kernel itself must not require twig/twig: se7enxweb/twig replaces twig/twig,
so a twig/twig requirement would make Composer apply the twig/twig advisories to it.

Since 1.2.5 and 1.3.5 the requirement on PHP 8.1 and later is `twig/twig` `^3.27 || ~3.19.1`. A project
that requires se7enxweb/twig 3.19.1 itself (Exponential Platform Legacy 3.x does on every PHP version,
4.6.x allows it) meets it through the fork, which replaces twig/twig 3.19.1; nothing else can, because
upstream twig/twig 3.19 is blocked by its security advisories. Without such a project Composer still
chooses `twig/twig` 3.27 or later, the highest release that matches.

### GraphQL

The metapackage does not require `webonyx/graphql-php`, on any PHP range, although the kernel's GraphQL
API runs on it (version 15, `^15.32.3`). The platforms the kernel is installed into bring a GraphQL
library of their own for their GraphQL bundle, which cannot be installed next to `webonyx/graphql-php`
15: Exponential Platform Legacy 3.x installs `ibexa/graphql-php` 0.13 on every PHP version from 8.0, and
4.6.x on PHP 7.4 installs `se7enxweb/graphql-php` 14.11. Both replace `webonyx/graphql-php`. Checked with
Composer 2.10.3, security blocking on, on 31 October 2026: with `webonyx/graphql-php` `^15.32.3` added to
this metapackage, 4.6.x on PHP 7.4 and 3.x on PHP 8.0 and 8.1 could not be resolved.

The kernel lists the library under `suggest` and `require-dev` instead: the kernel installed on its own
(`composer create-project`, or `composer install` in a checkout) installs it on every PHP version from
7.4 to 8.5, 4.6.x on PHP 8.0 and later and 5.x install version 15 themselves, and anywhere else
`composer require webonyx/graphql-php:^15.32.3` adds it. Without it, or with a platform's 0.13 or 14,
only the kernel's GraphQL API is unavailable, and says why (`./console exp:graphql:status`).

## What is not available on PHP 7.4

On PHP 7.4 Composer leaves out what cannot run there, and the kernel says so instead of failing:

- **Exponential Velocity** (the application server) needs PHP 8.0. `exp:velocity start`
  refuses with a message on 7.4; Apache or nginx with PHP-FPM, and the built-in `php`
  engine, work as before.
- **Exponential Layouts** (explayouts), the expsite packages and the media site theme need PHP 8.0.
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
