function _composer_scripts() {
    local cmd commands cur ref subcmd;
    _get_comp_words_by_ref -n : cur

    COMPREPLY=()
    cmd="${COMP_WORDS[0]/#\~/$HOME}"
    subcmd="${COMP_WORDS[0]}"
    commands=$("$cmd" --no-ansi 2> /dev/null | sed '/script as defined in composer.json./d' | awk '/^ +[a-z]+/ { printf "%s ",$1 }')

    ref=" ${commands[@]} "
    for w in ${COMP_WORDS[@]}; do
        if [[ " $ref " =~ " $w " ]]; then
            subcmd=$w
            break
        fi
    done

    #
    # Complete the arguments to some of the commands.
    #
    if [ "$subcmd" != "${COMP_WORDS[0]}" ] ; then
        local opts=$("$cmd" "$subcmd" -h --no-ansi 2> /dev/null | tr -cs '[=-=][:alpha:]_' '[\n*]' | grep '^-')
        case "$subcmd" in
            "run-script")
                # Complete scripts for composer "run-script" command.
                local cfgargs=$("$cmd" --no-ansi 2> /dev/null | grep 'script as defined in composer.json' | awk '/^ +[a-z]+/ { print $1 }')
                ;;
            "update")
                # Complete package names listed in the require and
                # require-dev sections in the composer.json.
                # Exclude ext-* and php version requirements.
                if `command -v jq > /dev/null 2>&1`; then
                    local cfgargs=$(jq -r '.require + ."require-dev" | keys[]' composer.json 2> /dev/null | grep -v '^ext-' | grep -v '^php$')
                fi
                ;;
        esac
        COMPREPLY=( $(compgen -W "${opts} ${cfgargs}" -- ${cur}) )
        return 0
    fi


    if [[ "$cur" == -* ]]; then
        COMPREPLY=( $( compgen -W '-h -q -v -V -n -d \
            --help --quiet --verbose --version --ansi --no-ansi \
            --no-interaction --profile --no-plugins --working-dir' -- "$cur" ) )
    else
        COMPREPLY=( $(compgen -W "${commands}" -- ${cur}) )
    fi

    return 0
}

complete -F _composer_scripts composer composer.phar
