# Remixd

`remixd` is a tool that intend to be used with [Remix IDE](http://github.com/ethereum/browser-solidity) (aka. Browser-Solidity). It allows a websocket connection between
`Remix IDE` (web application) and the local computer.

Practically Remix IDE make available a folder shared by `remixd`.

More details are explained in this [tutorial](http://remix.readthedocs.io/en/latest/tutorial_remixd_filesystem.html).

Alternatively `remixd` can be used to setup a development environment that can be used with other popular frameworks like Embark, Truffle, Ganache, etc..

`remixd` needs `npm` and `node`

## INSTALLATION

`npm install -g remixd`

## HELP SECTION

```
  Usage: remixd -s <shared folder> --remix-ide https://remix.ethereum.org

  Provide a two-way connection between the local computer and Remix IDE.
  

  Options:

  --remix-ide  <url>                    URL of remix instance allowed to connect to this 
                                        web sockect connection
  -s, --shared-folder <path>            Folder to share with Remix IDE
  --read-only                           Treat shared folder as read-only (experimental)
  -h, --help                            output usage information

```

## SHARE A FOLDER

`remixd -s <absolute-path> --remix-ide https://remix.ethereum.org`

The current user should have `read/write` access to the folder (at least `read` access).

It is important to notice that changes made to the current file in `Remix IDE` are automatically saved to the local computer every 5000 ms. There is no `Save` action. But the `Ctrl-Z` (undo) can be used.

Furthermore :
 - No copy of the shared folder are kept in the browser storage.
 - It is not possible to create a file from `Remix IDE` (that might change).
 - If a folder does not contain any file, the folder will not be displayed in the explorer (that might change).
 - Symbolic links are not forwarded to Remix IDE.
 

 ---------------------------------------------------------------------------------------------------------------------------------------
## How to run
Create testing or some other folder
bin/remixd -s ./testing --remix-ide http://http://localhost:8080/ --forward-commands --permissions READ,WRITE

Open https://remix.ethereum.org/ (or other whitelisted origin) 
Right click on inspect 
Go to console

Inside a console type:

Remixd git flow:

ws=new WebSocket("ws://localhost:65520", "echo-protocol")

ws.onmessage = e => {
  console.log('Message from server:', event.data)
}

ws.send('{"id":1,"name":"git","key":"init");
ws.send('{"id":1,"name":"git","key":"clone","payload":"git@github.com:edisinovcic/remixd-test-repository.git"}');
ws.send('{"id":1,"name":"git","key":"add","payload":"."}');
ws.send('{"id":1,"name":"git","key":"commit","payload":"-m \'First commit\'}');
ws.send('{"id":1,"name":"git","key":"remote","payload":"add origin git@github.com:edisinovcic/remixd-test-repository.git"}');
ws.send('{"id":1,"name":"git","key":"push","payload":"-u origin master"}'); 

Or any other git command you want to run