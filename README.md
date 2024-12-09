# VPN Setup GitHub Action

This GitHub Action sets up and connects to a VPN on various operating systems, including Linux, macOS, and Windows. It uses the FortiClient VPN for secure connections.

## Inputs

| Name            | Description                       | Required | Default |
|-----------------|-----------------------------------|----------|---------|
| `vpn_ip`        | VPN server IP address            | Yes      | N/A     |
| `vpn_port`      | VPN server port                  | Yes      | N/A     |
| `vpn_username`  | VPN username                     | Yes      | N/A     |
| `vpn_password`  | VPN password                     | Yes      | N/A     |

## Outputs

This action does not provide any explicit outputs. You can verify the VPN connection status from the logs.

## Example Usage

```yaml
name: VPN Setup Example

on:
  push:
    branches:
      - main

jobs:
  vpn-setup:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, macos-latest, windows-latest]

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up VPN
        uses: myusp/connect-forticlient-vpn@main
        with:
          vpn_ip: ${{ secrets.VPN_IP }}
          vpn_port: ${{ secrets.VPN_PORT }}
          vpn_username: ${{ secrets.VPN_USERNAME }}
          vpn_password: ${{ secrets.VPN_PASSWORD }}
```

## Platform Compatibility

- **Tested**:
  - Ubuntu: ✔️
  - macOS: None
  - Windows: None

This action supports the following platforms:

- **Linux (Ubuntu)**: Installs FortiClient VPN using `apt-get` and configures it via `expect` scripts.
- **macOS**: Installs required dependencies using Homebrew and sets up FortiClient VPN (adjust installation steps as needed).
- **Windows**: Downloads and installs the FortiClient executable, then configures it using PowerShell scripts.

## Notes

- Ensure you add the required secrets (`VPN_IP`, `VPN_PORT`, `VPN_USERNAME`, `VPN_PASSWORD`) to your repository or environment settings for secure usage.
- Modify the platform-specific setup logic in the action if using a different VPN client or configuration.

## Contributing

Feel free to open issues or submit pull requests to improve the action or expand its functionality.

## License

This project is licensed under the [MIT License](LICENSE).

