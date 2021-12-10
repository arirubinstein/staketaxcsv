
# Reference Notes

  * Random notes, hopefully helpful on occasion.  Probably not helpful on first look.

# Python Linter
```
# run linter (configuration found in setup.cfg)
pycodestyle
```

# Unit Tests

You may notice a lack of unit tests in this codebase.  Though tests exist, I omitted them because they rely on extensive
use of real world wallet data.  For the sake of all users' privacy, I do not include these tests.  I'm open to 
ideas for alternatives, since obviously this is non-optimal.
  
# Ideal Configuration

Default code was made to work out of the box.  These are changes that require manual
actions.  They improve reliability (RPC Node settings) or speed (DB Cache) when compared to
default version.

## RPC Node settings

  * Default `sample.env` points to public RPC nodes.  This generally works, up to a point.
  * Edit/uncomment `sample.env` to change to point to more reliable private RPC node(s).
    * Examples for private RPC nodes (Figment, Quicknode) are included.

## DB Cache

Use of a database for caching is ideal to speed up certain RPC queries (especially SOL).  Here is
the script usage to use caching:

  ```
  # --cache flag requires implementation of Cache class (common/cache.py)
  python3 report_terra.py <wallet_address> --cache
  ```

To enable --cache, you must configure an aws connection for the boto3 code found in common/Cache.py.
  * One method: `aws configure`
    * See here to install AWS CLI: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
    * See here to use `aws configure`: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html
    
Alternatively, you may implement your own Cache class (common/cache.py).

# Installing python 3.9 on MacOS

  * Personal method--google is probably better 

    ```
    # Install brew (see https://brew.sh/)
    
    # python 3.9.9
    brew install openssl readline sqlite3 xz zlib
    pyenv install 3.9.9
    
    # use virtualenv
    brew install virtualenv
    virtualenv -p .pyenv/versions/3.9.9/bin/python3.9 env
    source env/bin/activate
    
    # install pip packages (same as README.md)
    pip3 install -r requirements.txt
    ```