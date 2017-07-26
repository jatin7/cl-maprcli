# cl-maprcli

## overview
This project is binding for maprcli and REST binding for Common Lisp. 

`maprcli` is tool for the command-line interface (CLI). And MapR provides REST API by making REST requesting programmatically or in a browser. Please refer to http://maprdocs.mapr.com/home/ReferenceGuide/maprcli-REST-API-Syntax.html

## install
cl-maprcli can be installed by quicklisp. 

```
mkdir develop
cd develop
git clone https://github.com/incjung/cl-maprcli.git
```
then in repl session
```
(push #p"~/development/swagger/cl-maprcli/" asdf:*central-registry*)
(ql:quickload :cl-maprcli)
```

## examples


### usages1

MapR's `maprcli` syntax is 
```
maprcli <command> [<subcommand>...] ?<parameters>
```

For example, if you want to get information about the specified volume, `maprcli` command can be used.  

```
maprcli volume info
    [ -cluster <cluster name> ]
    [ -output terse | verbose ]
    [ -path <mount directory> ]
    [ -name <volume name> ]
    [ -columns <column name> ]
```

You must specify either name or path, but not both. 

```
maprcli volume info -path /
```

`cl-maprcli` is 

```
(<command>-?<subcommand> :param-name <param-value>... :host *host* :output :pretty)
```
:host is mcs host 
:output can be `:pretty`, `:json`, `:list`.
 - :pretty is used if result has `data` field.
 - :json is returning json format
 - :list is default

You can get same information with 
```
(volume-info :path "/")

(volume-create :path "/test07" :name "helloworld")
(volume-info :path "/test07")

```
or if you want to get information from another remote server 
```
(volume-info :host "https://192.168.2.51:8443/rest" :path "/")
```
:host is mcs host. Or You can change host with `set-host` and the authorization id/pw with `set-authorization`

```
(set-host "https://192.168.2.51:8443/rest")
```



### support help page
For example, when you want to knwo "alarm list", then 
```
(help :/alarm/list)
```
