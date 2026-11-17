# block-named-access
A PoC Chromium implementation for `block-named-access`, a new CSP directive for turning off the named access feature of the  HTML spec, effectively eliminating DOM clobbering vulnerabilities.

# Setup #
- Check out and build Chromium commit **`b2bcc611eb581bba742f8bc6d0f6b03b1b5398f1`**
  - Follow the [official instructions](https://chromium.googlesource.com/chromium/src/+/main/docs/linux/build_instructions.md#System-requirements) and the [instructions for building older revisions](https://chromium.googlesource.com/chromium/src/+/main/docs/building_old_revisions.md).
  - Place the `args.gn` file included in this repo in your checkout's `out/Default` directory for a faster build.
  - **Note:** This should take several hours.
- Run the built executable to ensure everything is OK: `$ out/Default/chrome --no-sandbox`
- Apply the `block_named_access.patch` file from this repo to make all necessary changes for the `block-named-access` CSP directive:
  - `$ cd /path/to/chromium/checkout/src/`
  - `$ git apply --check /path/to/block_named_access.patch` (this should return no errors)
  - `$ git apply --reject --whitespace=fix /path/to/block_named_access.patch`
- Rebuild: `autoninja -C out/Default chrome`
- Launch modified Chromium: `$ out/Default/chrome --no-sandbox`
- Visit the [test page](https://kostasdrk.github.io/block-named-access/) that demonstrates the directive's enforcement and reporting capabilities.
  - You can launch an unmodified Chromium alongside the modified one to observe the differences.
