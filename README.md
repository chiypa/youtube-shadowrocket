# YouTube Shadowrocket

English | [简体中文](README.zh-CN.md)

A Shadowrocket configuration adapted from [Maasea/sgmodule](https://github.com/Maasea/sgmodule), with setup and troubleshooting instructions.

User feedback confirms that the configuration can filter some YouTube ads, but occasional ads may still appear. Results can vary with YouTube changes, your account, region, and app version.

## Installation

In Shadowrocket, open **Config → Modules → +**, paste the following URL, and download the module:

```text
https://raw.githubusercontent.com/chiypa/youtube-shadowrocket/main/YouTube.Enhance.Shadowrocket.sgmodule
```

Enable the module. Disable other modules that process the same YouTube requests to avoid duplicate processing.

## HTTPS decryption

This module requires HTTPS decryption for the specified YouTube domains so its request and response scripts can run.

1. Open the HTTPS decryption settings for your active Shadowrocket configuration and enable decryption.
2. Follow Shadowrocket's prompts to generate and install a CA certificate.
3. In iOS, go to **Settings → General → About → Certificate Trust Settings**, and enable full trust for the Shadowrocket certificate you just installed.
4. Confirm that both remote script files downloaded successfully. The module has three script entries; two use the same file.
5. Reconnect Shadowrocket, fully close YouTube, and reopen it.

Only install and trust certificates you generated for your own devices. This project does not distribute certificates or private keys.

## Changes in this configuration

- Replaces upstream argument templates with fixed values and retains the enclosing quotes around `argument`.
- Adjusts the `initplayback` pattern to match `ack` when it is the first query parameter.
- Retains the ad-domain blocking rules and UDP port 443 blocking rule from the existing adapted configuration.
- Sets `debug:false` by default to reduce debug output.

The fixed settings disable caption translation, hide the upload and clip buttons, and keep the Shorts button visible.

The ad-filtering scripts are still loaded directly from Maasea's upstream repository. This repository does not bundle or independently implement the script core. The remote scripts follow upstream updates and are not pinned to a specific revision.

## Performance and troubleshooting

- For everyday use, you can turn off Shadowrocket's proxy logging. Disabling this module's debug output does not disable Shadowrocket's own logging.
- HTTPS decryption and script processing add processing overhead.
- The retained UDP port 443 blocking rule applies to all destination domains. It affects other apps using that port and may add connection fallback overhead.
- If loading feels slower, compare logging on and off while keeping your proxy node, network, and module unchanged.
- If ads still appear, check HTTPS decryption, certificate trust, and script download status, then inspect script execution logs.

Do not publicly share complete proxy logs, browsing records, proxy subscription URLs, certificates, or private keys. When reporting an issue, include your OS and app versions, the type of ad, and relevant error messages with personal information removed.

## Validation status

The adapted configuration received user feedback on October 22, 2026: ad filtering worked, although some ads remained. Publication files were prepared and debug output was disabled by default on October 24, 2026. The parameters passed static checks; publication preparation did not include another on-device test.

The English documentation and module descriptions were added on October 24, 2026. This translation does not change the filtering rules, script settings, or installation URL.

## Credits and license

- Upstream project and processing scripts: [Maasea/sgmodule](https://github.com/Maasea/sgmodule)
- Original module: [YouTube.Enhance.sgmodule](https://github.com/Maasea/sgmodule/blob/master/YouTube.Enhance.sgmodule)
- This repository: [chiypa/youtube-shadowrocket](https://github.com/chiypa/youtube-shadowrocket)

Distributed under the Apache License 2.0, with upstream attribution and notices of configuration changes. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
