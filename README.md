# EctoOracleAdapter


## Install OSX
### Instant Client


Download appropriate version from Oracle and unzip. 
 mkdir -p /usr/local/Oracle/product/instantclient/11.2.0.4.0/bin  

 mkdir -p /usr/local/Oracle/product/instantclient/11.2.0.4.0/lib  

 mkdir -p /usr/local/Oracle/product/instantclient/11.2.0.4.0/jdbc/lib  

 mkdir -p /usr/local/Oracle/product/instantclient/11.2.0.4.0/rdbms/jlib  

 mkdir -p /usr/local/Oracle/product/instantclient/11.2.0.4.0/sqlplus/admin  

 mv ojdbc* /usr/local/Oracle/product/instantclient/11.2.0.4.0/jdbc/lib/
 mv x*.jar /usr/local/Oracle/product/instantclient/11.2.0.4.0/rdbms/jlib/
 mv glogin.sql /usr/local/Oracle/product/instantclient/11.2.0.4.0/sqlplus/admin/
 mv *dylib* /usr/local/Oracle/product/instantclient/11.2.0.4.0/lib/ 
 mv *README /usr/local/Oracle/product/instantclient/11.2.0.4.0/
 mv * /usr/local/Oracle/product/instantclient/11.2.0.4.0/bin/

 cd /usr/local/bin
 ln -s ../Oracle/product/instantclient/11.2.0.4.0/bin/sqlplus sqlplus

 cd /usr/local/Oracle/product/instantclient/11.2.0.4.0
 mkdir -p share/instantclient
 cd /usr/local/share
 ln -s ../Oracle/product/instantclient/11.2.0.4.0/share/instantclient/ instantclient

 echo "export ORACLE_BASE=/usr/local/Oracle \
       export ORACLE_HOME=$ORACLE_BASE/product/instantclient/11.2.0.4.0 \
       export DYLD_LIBRARY_PATH=$ORACLE_HOME/lib \
       export TNS_ADMIN=$ORACLE_BASE/admin/network" >> /usr/local/share/instantclient/instantclient.sh 

echo "source /usr/local/share/instantclient/instantclient.sh" >> ~/.zhrc

Based on this post




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
