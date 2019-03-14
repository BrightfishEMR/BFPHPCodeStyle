## Windows
- Download PHP7 and extract it to C:\PHP
- Add C:\PHP to PATH
- Download PEAR from https://pear.php.net/manual/en/installation.getting.php and save go-pear.phar to C:\PHP
- Start an elevated cmd in C:\php and run `php go-pear.phar`
- Import the generated .reg file into your windows registry (Should be in  C:\PHP)
- Run the following from within the elevated cmd promp: ```pear install PHP_CodeSniffer```
- Checkout https://github.com/BrightfishEMR/BFPHPCodeStyle.git to C:\BFPHPCodeStyle
- Run ```phpcs --config-set installed_paths C:\BFPHPCodeStyle```
- Run ```phpcs --config-set default_standard BF```

## OSX

```bash
# Ensure xcode is installed with xcode command line tools, note: this might spawn a prompt
xcode-select --install

# Install PHP 7.3 (includes pear)
brew install php@7.3

# Only needed on fresh install, link php@7.3 to path
brew link php@7.3 --force

# Add pear to the include path
echo 'include_path = ".:'$(pear config-get php_dir)'"' | sudo tee -a $(php -r 'echo php_ini_loaded_file();')

# Install PHP_CodeSniffer
sudo pear install PHP_CodeSniffer

# Relink to add phpcs to path
brew unlink php@7.3 && brew link php@7.3 --force

# Delete the existing dir if exists
sudo rm -rf ~/BFPHPCodeStyle/ 2> /dev/null

# Clone the BF coding standard into correct location
git clone https://github.com/BrightfishEMR/BFPHPCodeStyle.git ~/BFPHPCodeStyle/

# Add the standard to the sniffers path and set it as the default standard
sudo phpcs --config-set installed_paths ~/BFPHPCodeStyle/BF
sudo phpcs --config-set default_standard BF
```

## Install Sublime packages

- EditorConfig
- SublimeLinter
- SublimeLinter-php
- SublimeLinter-phpcs

Restart SublimeText.

### Sublime config

#### User
````
{
    "trim_trailing_white_space_on_save": true,
    "ensure_newline_at_eof_on_save": true,
    "trim_automatic_white_space": true,
    "translate_tabs_to_spaces": true,
    "default_line_ending": "unix",
    "tab_size": 4
}
````

#### Package - SublimeLinter - User
````
{
    "linters": {
        "php": {
            "@disable": false,
            "args": [],
            "excludes": []
        },
        "phpcs": {
            "@disable": false,
            "args": [],
            "excludes": [],
            "standard": "BF"
        }
    }
}
````

Note: The first time you save the "SublimeLinter - User" preferences and restart sublime it will reset the config file
