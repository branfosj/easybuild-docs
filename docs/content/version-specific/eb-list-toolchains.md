# Output of `eb --list-toolchains` {: #toolchains_table }

!!! warning
    This page will soon replace <https://docs.easybuild.io/en/latest/eb_list_toolchains.html>.

    **
    It still needs to be ported from *reStructuredText* (.rst) to *MarkDown* (.md),  
    and you can help with that!
    **

    - source: [`docs/eb_list_toolchains.rst` in `easybuilders/easybuild` repo](https://raw.githubusercontent.com/easybuilders/easybuild/develop/docs/eb_list_toolchains.rst)
    - target: [`docs/version-specific/eb-list-toolchains.md` in `easybuilders/easybuild-docs` repo](https://github.com/easybuilders/easybuild-docs/tree/main/docs/version-specific/eb-list-toolchains.md)

    See <https://github.com/easybuilders/easybuild-docs> for more information.

```rst

.. _toolchains_table:

List of known toolchains
========================

The list of known toolchains can easily be obtained with::

  $ eb --list-toolchains
  List of known toolchains (toolchainname: module[,module...]):
  [...]

An up-to-date overview of known toolchains is available at :ref:`vsd_list_toolchains`.

.. note:: The `system` toolchain is a special case, see :ref:`system_toolchain`.

```
