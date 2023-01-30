# How to make you own templates

Sometimes we want to make our templates and add variables to it. This can be done with `sed` command. `sed` gives us the ability to change reemplace words/tokens. An example can be:

```bash
PATH_SERVICE="${DIR}/services/files/gunicorn.service"
PROJECT_NAME=$(basename -- $(dirname --  $(find $DIR -name wsgi.py)))
USER=$(whoami)

trap "rm -f ${PATH_SERVICE}" EXIT # Erase temp files

sed -e "s|\${DIR}|${DIR}|" \
    -e "s|\${PROJECT_NAME}|${PROJECT_NAME}" \
    "${DIR}/services/templates/gunicorn.service" \
    >| ${PATH_SERVICE}

```
Note that the `-e` option gives the option to use small script with the secuences we want to remplace. So basically the syntax in this example is: `sed -e "s|\s${<token>|$<yourVar>|}" ... <path_to_template> |> <path_to_newFile> ` the `>|` is the nonclober operator this avoit to manage errors.


# Erasing temporaly files

Sometimes is necessary to generate files to config the enviroment but this files must to be rid off at the end of the process. This can be done with:

```bash
trap "rm -f <${PATH_toFile}>" EXIT
```

The `EXIT` is a special signal to inform to `trap` comman  when do the action traped between the "".


# Obtain the parent dir relative to the script running

To obtain the dir relative to the script can be done with this simple command.

```bash
DIR=$(cd -- "$(dirname -- "{BASH_SOURCE[0]"})" &> /dev/null && pwd)
```
