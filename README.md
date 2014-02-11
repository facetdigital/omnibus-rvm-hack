omnibus-rvm-hack Cookbook
===========================

This cookbook makes the Chef Omnibus installer work when RVM is loaded by the root user.

This is a workaround for the known bug [CHEF-3581](https://tickets.opscode.com/browse/CHEF-3581) that prevents `chef-client`, `chef-solo`, and other Chef commands from running properly when they are installed with the Omnibus installer, and you already have RVM installed and loaded. The technique used here is to overwrite the `/usr/bin` symlinks that link to the Omnibus executables, with a script that wraps those executables, and executes them after clearing out `GEM_HOME` and `GEM_PATH` environment variables, as discussed in the comments on [CHEF-3581](https://tickets.opscode.com/browse/CHEF-3581), such that the RVM environment is not incidentially used.

This comes in useful, for example, when you provision a Vagrant VM with Chef Solo, installed via Omnibus, that has a recipe that installs RVM and loads it for the root user. In a scenario like that, your node will come up but the next `chef-solo` or `vagrant provision` run will fail in Chef. This cookbook works around this problem.

Usage
-----
#### omnibus-rvm-hack::default

Just include `omnibus-rvm-hack` in your node's `run_list`:

```json
{
  "name":"my_node",
  "run_list": [
    "recipe[omnibus-rvm-hack]"
  ]
}
```

Contributing
------------

1. Fork the repository on Github
2. Create a named feature branch (like `add_component_x`)
3. Write your change
4. Write tests for your change (if applicable)
5. Run the tests, ensuring they all pass
6. Submit a Pull Request using Github

License and Authors
-------------------
Authors: Scott W. Bradley <scottwb@gmail.com>
