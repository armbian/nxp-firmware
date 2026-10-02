# NXP firmware mirror

Read-only mirror of the NXP i.MX firmware packages used by the [Armbian build framework](https://github.com/armbian/build).
Some build hosts cannot reach `www.nxp.com`; this repository serves the same files from GitHub.

Each package has its own branch. A branch holds the unmodified `.bin` files from
`https://www.nxp.com/lgfiles/NMG/MAD/YOCTO/` and a `SHA256SUMS` file:

| Branch | Example download |
|---|---|
| `firmware-imx` | `https://github.com/armbian/nxp-firmware/raw/firmware-imx/firmware-imx-8.26-d4c33ab.bin` |
| `firmware-ele-imx` | `https://github.com/armbian/nxp-firmware/raw/firmware-ele-imx/firmware-ele-imx-2.0.2.1-d30b14a.bin` |
| `firmware-sentinel` | `https://github.com/armbian/nxp-firmware/raw/firmware-sentinel/firmware-sentinel-0.10.bin` |
| `firmware-upower` | `https://github.com/armbian/nxp-firmware/raw/firmware-upower/firmware-upower-1.3.0.bin` |

## How it updates

`.github/workflows/sync-mirror.yml` runs daily on GitHub's runners. It collects the
package names referenced in armbian/build `main` (`config/sources/families`), adds
the names listed in `mirror.list`, and downloads every file that is not mirrored yet.

The mirror is add-only. Files are never replaced or removed, so older Armbian
branches keep working. If NXP changes a file under an existing name, the sync fails
instead of overwriting it.

## License

The files belong to NXP and are distributed under the NXP Software License Agreement.
Each package is a self-extracting archive that shows the agreement before it unpacks;
by extracting it you accept that agreement.
