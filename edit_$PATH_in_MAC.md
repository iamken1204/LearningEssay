# Add $PATH in mac

1. Open `~/.bash_profile`
2. Add `export PATH="the_path_to_your_command_file:$PATH"`
3. Save
If the path is under `~/`, use `$HOME` to replace `~/`.

ex:   
```shell
# Add `homestead` to the `$PATH`
export PATH="$HOME/.composer/vendor/bin/:$PATH";
```
