# Deprecated functionality {: #deprecated }

Some of the functionality that was available in previous EasyBuild
versions is *deprecated*, and should no longer be used.

This functionality will be removed in a future version of EasyBuild (see
[Removed functionality][removed_functionality] for more
information about functionality that has been removed already).

This page:

- provides an
    [Overview of deprecated functionality in EasyBuild version][overview_deprecated] together with available alternatives
- describes the
    [Deprecation policy][deprecation_policy]
- explains how to easily
    [check for use of deprecated functionality][how_to_check_use_of_deprecated_functionality]

## Overview of deprecated functionality in EasyBuild version {: #overview_deprecated }

The different section below document the functionality that is
deprecated in EasyBuild version, for which support will be removed in
EasyBuild version 5.0.

For EasyBuild users:

- [Support for using Lmod 6.x][depr_lmod6]

For authors of easyconfig files:

- [`dummy` toolchain][depr_dummy_toolchain]

For developers of easyblocks:

*(nothing yet)*

For EasyBuild framework developers:

*(nothing yet)*

### Support for using Lmod 6.x {: #depr_lmod6 }

- *deprecated since:* EasyBuild v4.1.0 (Nov'19)
- *removed in:* EasyBuild v5.0
- *alternative(s)*: **use Lmod 7.x or more recent**

Support for using Lmod 6.x as modules tool with EasyBuild has been
deprecated, and will be removed in a future version of EasyBuild.

### `dummy` toolchain {: #depr_dummy_toolchain }

- *deprecated since:* EasyBuild v4.0.0 (Sept'19)
- *removed in:* EasyBuild v5.0
- *alternative(s)*: **use** `system` **toolchain instead**

The `dummy` toolchain is has been deprecated, and is replaced with the
`system` toolchain.

For more information, see [System toolchain][system_toolchain].

## Deprecation policy {: #deprecation_policy }

With every EasyBuild release, we try very hard to maintain *backward
compatibility*. That is, EasyBuild version `X.Y` should still build
software packages that could be built with EasyBuild version `X.(Y-1)`,
without requiring modifications to the used easyconfig file or
easyblock.

However, every now and then a breaking change needs to be made to
EasyBuild, because of design decisions or to resolve mistakes that were
made in the past. These changes involve *deprecating* the behaviour or
functionality we want to get rid of, together with supporting a better
alternative.

**Deprecating functionality:**

- using a `log.deprecated("msg", 'X.Y')` statement in EasyBuild
    version `X.(Y-n)` a certain block of code is tagged as *deprecated*,
    indicating that the corresponding functionality will no longer be
    supported in EasyBuild version `X.Y`; for example, to deprecate the
    use of the `makeopts` easyconfig parameter with EasyBuild v2.0:

    ``` python
    if self.cfg['makeopts']:
        self.log.deprecated("Easyconfig parameter 'makeopts' is deprecated, use 'buildopts' instead", '2.0')
    ```

- until EasyBuild version `X.Y`, the deprecation log message will
    manifest itself as a *warning*, highlighting the use of deprecated
    functionality; for example:

    ``` console
    == 2014-12-16 16:29:07,906 main.easyconfig.easyconfig WARNING Deprecated functionality, will no longer work in v2.0:
    Easyconfig parameter 'makeopts' is deprecated, use 'buildopts' instead;
    see http://easybuild.readthedocs.org/en/latest/Deprecated-functionality.html for more information
    ```

**Removing support for deprecated behavior:**

- starting with EasyBuild version `X.Y`, the deprecation log message
    will result in an *error*, indicating that the deprecated behavior
    is no longer supported; for example:

    ``` console
    ERROR: EasyBuild encountered an exception (at easybuild/framework/easyconfig/easyconfig.py:937 in process_easyconfig):
    Failed to process easyconfig /home/example/gzip-1.5-goolf-1.4.10.eb:
    DEPRECATED (since v2.0) functionality used: Easyconfig parameter 'makeopts' is deprecated, use 'buildopts' instead;
    see http://easybuild.readthedocs.org/en/latest/Deprecated-functionality.html for more information.
    ```

- the code supporting the deprecated functionality is *removed* in
    EasyBuild version `X.(Y+1)` (i.e., the first non-bugfix-only release
    after version `X.Y`), see also
    [Removed functionality][removed_functionality]

- until EasyBuild version `X.(Y+1)`, the code supporting the
    deprecated functionality will still be available; using the
    `--deprecated` command line option (or, equivalently, the
    `$EASYBUILD_DEPRECATED` environment variable), the deprecated
    functionality can be reactivated by specifying a *lower* version;
    for example, to avoid running into an error with EasyBuild v2.0 for
    functionality that was deprecated for EasyBuild v2.0:

    ``` shell
    eb gzip-1.5-goolf-1.4.10.eb --deprecated=1.0
    ```

## How to check for use of deprecated functionality {: #how_to_check_use_of_deprecated_functionality }

Since EasyBuild v1.16.0, the `--deprecated` command line option can be
used to check whether deprecated behavior is still being triggered in
your EasyBuild setup.

For example, using `--deprecated=5.0` with EasyBuild v4.x will transform
any deprecation warning for functionality that will no longer be
supported in EasyBuild v5.0 into an error message. For example:

``` console
$ eb test.eb --deprecated=5.0
== temporary log file in case of crash /tmp/easybuild-WWalWX/easybuild-aoL9Nd.log
ERROR: Failed to process easyconfig /home/example/test.eb:
DEPRECATED (since v5.0) functionality used: Use of 'dummy' toolchain is deprecated, use 'system' toolchain instead;
see http://easybuild.readthedocs.org/en/latest/Deprecated-functionality.html for more information
be used; see http://easybuild.readthedocs.org/en/latest/Deprecated-functionality.html for more information
```

!!! tip
    Define `deprecated` to the next major EasyBuild version in one of your EasyBuild configuration files
    (see [Configuration file(s)][configuration_file]) or by
    defining `$EASYBUILD_DEPRECATED=5.0`, to ensure you are made aware
    of deprecated behavior as early as possible.

    You can (temporarily) still rely on the deprecated functionality by
    specifying a *lower* version via `--deprecated` to overrule that
    setting, until the functionality is actually disabled.
