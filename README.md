# LuCI QFirehose Application

A LuCI web interface for QFirehose (v1.4.17), providing a user-friendly way to flash Qualcomm firmware on Quectel modems via OpenWrt.

https://pcat.qsim.top/readme/Luci-app-qfirehose%202.1.0.MP4

## Features

- Modern custom DOM layout with LuCI theme compatibility
- Modem model and current firmware display (via AT commands)
- Firmware upload with progress bar
- Supports firmware directory, `.zip` and `.7z` packages (built-in decompression in v1.4.17)
- Automatic USB/PCIe device detection with refresh button
- Real-time log monitoring (terminal-style dark theme)
- Support for multiple USB ports and devices
- Device type selection (NAND/eMMC/UFS)
- Collapsible advanced options: MD5 skip, signed firmware, USBMon log capture, full erase
- Editable firmware path for manual input
- Reset button for clearing state after flash
- Automatic completion/failure detection with status indicator

## Supported Modules

QFirehose v1.4.17 supports a wide range of Quectel modules including:

- EC20, EC25, EG25, EG06, EM05, EM06, EM12, EM20
- AG35, AG520R, AG525, AG550, AG590
- AG215S-GLR, AG215S-GLBA
- RM500Q, RM520N, RG500Q, RG520N
- SC600Y-EM, SC60-CE
- And more...

## Dependencies

- luci-base
- cgi-io (firmware upload)
- qfirehose (v1.4.17, includes unzip and p7zip dependencies)
- socat (AT command communication for modem info)

## Installation

1. Add this repository to your OpenWrt build system

2. Build the package:

```bash
make package/luci-app-qfirehose/compile V=s
```

3. Install the generated package on your OpenWrt device:

```bash
opkg install luci-app-qfirehose_2.0.0_all.ipk
```

## Usage

1. Access your OpenWrt LuCI web interface
2. Navigate to Modem -> QFirehose
3. Upload your firmware file (directory, .zip or .7z)
4. Configure options (port, device, storage type, etc.)
5. Click "Flash Firmware" to start
6. Monitor the progress through the log window

## Changelog

### v2.1.0 (2026-02-15)

- **UI Rewrite**: Replaced `form.Map` with custom DOM layout using LuCI native `cbi-*` classes for full theme compatibility
- **Modem Info**: Added modem model and current firmware display via AT commands (`ATI`, `AT+QGMR`) using socat
- **Upload Progress**: Added real-time upload progress bar for firmware files
- **Refresh Button**: "Refresh Devices" button now also refreshes modem model and firmware info
- **Advanced Options**: Collapsible section with MD5 skip, signed firmware, USBMon log capture (`-u`), and full erase
- **Editable Path**: Firmware path input is now editable for manual entry
- **Reset Button**: Added reset button to clear state after flash completion/failure
- **Log Viewer**: Terminal-style dark theme with placeholder text
- **Real-time Logging**: Direct stdout/stderr redirect (removed `tee` pipe) for immediate log updates
- **Status Script**: Simplified to plain text output, removed fragile JSON parsing
- **ACL**: Updated permissions for all scripts including `qfirehose-modem-info`
- **Translations**: Full Chinese (zh-Hans) translation coverage

### v2.0.0

- Upgraded QFirehose from v1.2 to v1.4.17
- Added support for zip/7z firmware packages (built-in decompression)
- Added device type selection (NAND/eMMC/UFS)
- Added signed firmware support (-v flag)
- Added PCIe device detection (mhi/wwan)
- Fixed parameter passing in flash command
- Simplified start script (removed manual unzip logic)
- Improved log polling and status detection
- Cleaned up ACL permissions and init script

## License

This project is licensed under the GPLv3 License - see the LICENSE file for details.

## Author

- Zag (<ntbowen2001@gmail.com>)
- Homepage: <https://pcat.qsim.top>

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
