# EctoOracleAdapter


## Install OSX
## Instant Client
Download appropriate version from Oracle and unzip. [link](http://www.oracle.com/technetwork/topics/intel-macsoft-096467.html)
```
1. 
    unzip -qq instantclient-basic-macos.x64-12.1.0.2.0.zip
    unzip -qq instantclient-sqlplus-macos.x64-12.1.0.2.0.zip
    unzip -qq instantclient-tools-macos.x64-12.1.0.2.0.zip
    unzip instantclient-sdk-macos.x64-12.1.0.2.0.zip

2.     
    mkdir -p /Applications/oracle/product/instantclient_64/12.1.0.2.0/bin  
    mkdir -p /Applications/oracle/product/instantclient_64/12.1.0.2.0/lib  
    mkdir -p /Applications/oracle/product/instantclient_64/12.1.0.2.0/jdbc/lib
    mkdir -p /Applications/oracle/product/instantclient_64/12.1.0.2.0/rdbms/jlib/
    mkdir -p /Applications/oracle/product/instantclient_64/12.1.0.2.0/dbms/jlib  
    mkdir -p /Applications/oracle/product/instantclient_64/12.1.0.2.0/sqlplus/admin
    mkdir -p /Applications/oracle/product/instantclient_64/12.1.0.2.0/network/admin

3. 
   cd instantclient_12_1
   mv ojdbc* /Applications/oracle/product/instantclient_64/12.1.0.2.0/jdbc/lib/
    mv x*.jar /Applications/oracle/product/instantclient_64/12.1.0.2.0/rdbms/jlib/
    mv glogin.sql /Applications/oracle/product/instantclient_64/12.1.0.2.0/sqlplus/admin/
    mv *dylib* /Applications/oracle/product/instantclient_64/12.1.0.2.0/lib/ 
    mv *README /Applications/oracle/product/instantclient_64/12.1.0.2.0/
    mv sdk /Applications/oracle/product/instantclient_64/12.1.0.2.0/sdk
    mv * /Applications/oracle/product/instantclient_64/12.1.0.2.0/bin/

4. 
    cd /usr/local/bin
    ln -s /Applications/oracle/product/instantclient_64/12.1.0.2.0/bin/sqlplus sqlplus

5. 
    cd /Applications/oracle/product/instantclient_64/12.1.0.2.0
    mkdir -p share/instantclient
    cd /usr/local/share
    ln -s /Applications/oracle/product/instantclient_64/12.1.0.2.0/share/instantclient/ instantclient
```
### ~/.bash_profile
``` 
# Oracle
export ORACLE_BASE=/Applications/oracle
export ORACLE_HOME=$ORACLE_BASE/product/instantclient_64/12.1.0.2.0
export PATH=$ORACLE_HOME/bin:$PATH
export DYLD_LIBRARY_PATH=$ORACLE_HOME/lib
export TNS_ADMIN=$ORACLE_HOME/network/admin
export export NLS_LANG="AMERICAN_AMERICA.UTF8"
# Oracle SDK
export OCI_LIB_DIR=$ORACLE_HOME/lib
export OCI_INC_DIR=$ORACLE_HOME/sdk/include
export INSTANT_CLIENT_LIB_PATH=$ORACLE_HOME/lib
export INSTANT_CLIENT_INCLUDE_PATH=$ORACLE_HOME/sdk/include
# Erlang 
export ERL_INTERFACE_DIR=/usr/local/lib/erlang/lib/erl_interface-3.9.3
```    
Load setting
```
source ~/.bash_profile
```
### TNS
```
nano $TNS_ADMIN/tnsnames.ora
```
tnsnames.ora
```
MYDB=
(DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=*********)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SID=MYDB-SID)
    )  
)
```
### Test client instalation
```
sqlplus user/pass@MYDB
```

## Driver dependencies

`cd $ORACLE_HOME/lib`

`ln -s {libclntsh.dylib.12.1,libnnz12.dylib,libociei.dylib} /usr/local/lib`

### Compile issues:
* `brew install libevent`
* `cd $INSTANT_CLIENT_LIB_PATH`
* `ln -s libocci.dylib.12.1  libocci.dylib`
* `ln -s libclntsh.dylib.12.1 libclntsh.dylib`

## if you have problem with `event.h` run:
`xcode-select --install`
## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed as:

  1. Add ecto_oracle_adapter to your list of dependencies in `mix.exs`:

        def deps do
          [{:ecto_oracle_adapter, "~> 0.0.1"}]
        end

  2. Ensure ecto_oracle_adapter is started before your application:

        def application do
          [applications: [:ecto_oracle_adapter]]
        end
