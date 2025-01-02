# Stow Package Inspector

A lightweight shell script to inspect the health and availability of stowed
packages managed with GNU Stow. This script provides detailed reports on the
status of your stowed packages, helping you identify conflicts, incomplete
stows, and unused packages in your stow directory.

## Features

- **Health Inspection**: Check the status of packages listed in
  `packages_to_stow` to identify:

  - **Conflicts**: Files or directories blocking symlink creation.
  - **Incomplete Stows**: Packages with partially missing symlinks.
  - **Not Stowed**: Packages listed but not yet stowed.
  - **Stowed**: Fully stowed packages (optional to include in reports).

- **Available Packages**: Identify directories in your stow directory that
  are not listed in `packages_to_stow`.

- **Customizable Reports**: Use flags to customize the scope of the
  inspection:
  - Focus on specific types of issues.
  - Include stowed packages.
  - View only available packages.

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/stonematt/stow-package-inspector.git
   cd stow-package-inspector
   ```

2. Make the script executable:

   ```bash
   chmod +x stow_check.sh
   ```

3. Ensure `stow` is installed on your system:

   ```bash
   sudo apt install stow   # For Debian/Ubuntu
   brew install stow       # For macOS
   ```

## Usage

```bash
./stow_check.sh [options]
```

### Options

| Option | Description                                                           |
| ------ | --------------------------------------------------------------------- |
| `-h`   | Display help and usage information.                                   |
| `-v`   | Enable verbose output (show the `stow` command being executed for     |
|        | each package).                                                        |
| `-f`   | Include available packages not listed in `packages_to_stow`.          |
| `-s`   | Include stowed packages in the `packages_to_stow` report.             |
| `-a`   | Show only available packages (ignore packages in `packages_to_stow`). |

### Examples

1. **Default Usage**:
   Inspect `packages_to_stow`, excluding fully stowed packages:

   ```bash
   ./stow_check.sh
   ```

2. **Full Report**:
   Include both `packages_to_stow` and available packages in the stow directory:

   ```bash
   ./stow_check.sh -f
   ```

3. **Include Stowed**:
   Include stowed packages in the `packages_to_stow` report:

   ```bash
   ./stow_check.sh -s
   ```

4. **Only Available**:
   Show only available packages in the stow directory:

   ```bash
   ./stow_check.sh -a
   ```

5. **Combine Options**:
   Generate a full report and include stowed packages:

   ```bash
   ./stow_check.sh -fs
   ```

## Requirements

- GNU Stow (`stow`)
- A `.stowrc` file with the following format:

  ```plaintext
  --dir=<path-to-stow-directory>
  --target=<target-directory>
  ```

- A `packages_to_stow` file listing the packages to be managed (one package
  per line):

  ```plaintext
  alacritty/
  git/
  vim/
  ```

## Output Examples

### Default Output

```plaintext
Checking packages in packages_to_stow...

Expected Packages from packages_to_stow:
conflict: aws
incomplete: git
not_stowed: alacritty
not_stowed: ripgrep
```

### Full Report (`-f`)

```plaintext
Checking packages in packages_to_stow...
Checking available packages not in packages_to_stow...

Expected Packages from packages_to_stow:
conflict: aws
incomplete: git
not_stowed: alacritty
not_stowed: ripgrep

Other available packages:
stowed: kitty
stowed: lsd
stowed: htop
```

## Contributing

Contributions are welcome! If you have ideas for new features or enhancements,
feel free to submit a pull request or open an issue.

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature-name`.
3. Commit your changes: `git commit -m "Add feature-name"`.
4. Push to your branch: `git push origin feature-name`.
5. Open a pull request.

## License

This project is licensed under the MIT License. See the `LICENSE` file for
details.

---

Feel free to reach out with any questions or suggestions!