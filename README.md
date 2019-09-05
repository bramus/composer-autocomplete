# Bash/Shell Autocompletion for Composer

[![Source](http://img.shields.io/badge/source-bramus/composer--autocomplete-blue.svg?style=flat-square)](https://github.com/bramus/composer-autocomplete) [![License](https://img.shields.io/github/license/bramus/composer-autocomplete.svg?style=flat-square)](https://github.com/bramus/composer-autocomplete/blob/master/LICENSE)

`composer-autocomplete` provides Bash/Shell autocompletion for Composer.

Built by Bram(us) Van Damme _([https://www.bram.us](https://www.bram.us))_ and [Contributors](https://github.com/bramus/enumeration/graphs/contributors)

## Prerequisites

If the `complete` command is not available on your system, you can install `bash-completion` using [Homebrew](https://brew.sh/)

```shell
brew install bash-completion
```


## Installation

1. Download the [file `composer-autocomplete`](composer-autocomplete) from this repo

	```shell
	curl -#L https://github.com/bramus/composer-autocomplete/tarball/master | tar -xzv --strip-components 1 --exclude={LICENSE,README.md}
	```

2. Move the file `composer-autocomplete` to `~`

	```shell
	mv ./composer-autocomplete ~/composer-autocomplete
	```

3. Load `composer-autocomplete` from within your `~/.bash_profile`

	Either manually add this snippet to your `~/.bash_profile`:

	```bash
	if [ -f "$HOME/composer-autocomplete" ] ; then
	    . $HOME/composer-autocomplete
	fi
	```

	Or use this set of commands to do it automatically:

	```shell
	echo "" >> ~/.bash_profile
	echo 'if [ -f "$HOME/composer-autocomplete" ] ; then' >> ~/.bash_profile
	echo '    . $HOME/composer-autocomplete' >> ~/.bash_profile
	echo "fi" >> ~/.bash_profile
	```

4. Restart your shell, or reload your `~/.bash_profile`

	```shell
	source ~/.bash_profile
	```


## Usage

To list `composer` commands:

```
$ composer [TAB][TAB]
about                clear-cache          create-project       dumpautoload         home                 install              prohibits            search               status               upgrade
archive              clearcache           depends              exec                 i                    licenses             remove               self-update          suggests             validate
browse               command              diagnose             global               info                 list                 require              selfupdate           u                    why
check-platform-reqs  config               dump-autoload        help                 init                 outdated             run-script           show                 update               why-not
```

To complete a `composer` commands:

```
$ composer in[TAB][TAB]
info     init     install
```

To list options for a `composer` command:

```
$ composer install -[TAB][TAB]
--                        --dev                     --no-ansi                 --no-interaction          --no-suggest              --profile                 --working-dir             -h                        -v
--ansi                    --dry-run                 --no-autoloader           --no-plugins              --optimize-autoloader     --quiet                   -V                        -n
--apcu-autoloader         --help                    --no-custom-installers    --no-progress             --prefer-dist             --verbose                 -a                        -o
--classmap-authoritative  --ignore-platform-reqs    --no-dev                  --no-scripts              --prefer-source           --version                 -d                        -q
```

To complete [Composer scripts](https://getcomposer.org/doc/articles/scripts.md) _(example)_:

```
$ composer run-script [TAB][TAB]
fix   lint  test
```

## Acknowledgements

This project builds upon [Rob Allen's previous work](https://akrabat.com/autocomplete-composer-script-names-on-the-command-line/) in this area.

## License

`composer-autocomplete` is released under the MIT public license. See the enclosed `LICENSE` for details.