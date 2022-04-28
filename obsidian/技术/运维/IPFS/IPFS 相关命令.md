# IPFS 相关命令

相关概念:
```

```


## 基本命令
```bash
# 初始化 
ipfs init

# 启动
ipfs daemon

# 查看本地文件
ipfs pin ls

# 上传文件/文件夹
ipfs add

# 查看文件
ipfs cat <hash>

# 下载文件
ipfs get <hash>

# 文件操作
ipfs files ls
ipfs files mkdir <path>
ipfs files write <path> <data>
ipfs files read <path>
ipfs files rm
ipfs files mv
ipfs files cp
ipfs files stat
```



## ipfs help
```
USAGE
  ipfs - Global p2p merkle-dag filesystem.

SYNOPSIS
  ipfs [--config=<config> | -c] [--debug=<debug> | -D] [--help=<help>] [-h=<h>] [--local=<local> | -L] [--api=<api>] <command> ...

OPTIONS

  -c,              --config   string - Path to the configuration file to use.
  -D,              --debug    bool   - Operate in debug mode.
  --help                      bool   - Show the full command help text.
  -h                          bool   - Show a short version of the command help text.
  -L,              --local    bool   - Run the command locally, instead of using the daemon.
  --api                       string - Use a specific API instance (defaults to /ip4/127.0.0.1/tcp/5001).
  --enc,           --encoding string - The encoding type the output should be encoded with (json, xml, or text). Default: text.
  --stream-channels           bool   - Stream channel output.
  --timeout                   string - set a global timeout on the command.

SUBCOMMANDS
  BASIC COMMANDS
    init          Initialize ipfs local configuration
    add <path>    Add a file to IPFS
    cat <ref>     Show IPFS object data
    get <ref>     Download IPFS objects
    ls <ref>      List links from an object
    refs <ref>    List hashes of links from an object
  
  DATA STRUCTURE COMMANDS
    block         Interact with raw blocks in the datastore
    object        Interact with raw dag nodes
    files         Interact with objects as if they were a unix filesystem
    dag           Interact with IPLD documents (experimental)
  
  ADVANCED COMMANDS
    daemon        Start a long-running daemon process
    mount         Mount an IPFS read-only mountpoint
    resolve       Resolve any type of name
    name          Publish and resolve IPNS names
    key           Create and list IPNS name keypairs
    dns           Resolve DNS links
    pin           Pin objects to local storage
    repo          Manipulate the IPFS repository
    stats         Various operational stats
    p2p           Libp2p stream mounting
    filestore     Manage the filestore (experimental)
  
  NETWORK COMMANDS
    id            Show info about IPFS peers
    bootstrap     Add or remove bootstrap peers
    swarm         Manage connections to the p2p network
    dht           Query the DHT for values or peers
    ping          Measure the latency of a connection
    diag          Print diagnostics
  
  TOOL COMMANDS
    config        Manage configuration
    version       Show ipfs version information
    update        Download and apply go-ipfs updates
    commands      List all available commands
```

## ifps add help
```
USAGE
  ipfs add <path>... - Add a file or directory to ipfs.

SYNOPSIS
  ipfs add [--recursive | -r] [--quiet | -q] [--quieter | -Q] [--silent] [--progress | -p] [--trickle | -t] [--only-hash | -n] [--wrap-with-directory | -w] [--hidden | -H] [--chunker=<chunker> | -s] [--pin=false] [--raw-leaves] [--nocopy] [--fscache] [--cid-version=<cid-version>] [--hash=<hash>] [--] <path>...

ARGUMENTS

  <path>... - The path to a file to be added to ipfs.

OPTIONS

  -r,          --recursive           bool   - Add directory paths recursively. Default: false.
  -q,          --quiet               bool   - Write minimal output.
  -Q,          --quieter             bool   - Write only final hash.
  --silent                           bool   - Write no output.
  -p,          --progress            bool   - Stream progress data.
  -t,          --trickle             bool   - Use trickle-dag format for dag generation.
  -n,          --only-hash           bool   - Only chunk and hash - do not write to disk.
  -w,          --wrap-with-directory bool   - Wrap files with a directory object.
  -H,          --hidden              bool   - Include files that are hidden. Only takes effect on recursive add.
  -s,          --chunker             string - Chunking algorithm, size-[bytes] or rabin-[min]-[avg]-[max]. Default: size-262144.
  --pin                              bool   - Pin this object when adding. Default: true.
  --raw-leaves                       bool   - Use raw blocks for leaf nodes. (experimental).
  --nocopy                           bool   - Add the file using filestore. Implies raw-leaves. (experimental).
  --fscache                          bool   - Check the filestore for pre-existing blocks. (experimental).
  --cid-version                      int    - CID version. Defaults to 0 unless an option that depends on CIDv1 is passed. (experimental).
  --hash                             string - Hash function to use. Implies CIDv1 if not sha2-256. (experimental). Default: sha2-256.

DESCRIPTION

  Adds contents of <path> to ipfs. Use -r to add directories.
  Note that directories are added recursively, to form the ipfs
  MerkleDAG.
  
  The wrap option, '-w', wraps the file (or files, if using the
  recursive option) in a directory. This directory contains only
  the files which have been added, and means that the file retains
  its filename. For example:
  
    > ipfs add example.jpg
    added QmbFMke1KXqnYyBBWxB74N4c5SBnJMVAiMNRcGu6x1AwQH example.jpg
    > ipfs add example.jpg -w
    added QmbFMke1KXqnYyBBWxB74N4c5SBnJMVAiMNRcGu6x1AwQH example.jpg
    added QmaG4FuMqEBnQNn3C8XJ5bpW8kLs7zq2ZXgHptJHbKDDVx
  
  You can now refer to the added file in a gateway, like so:
  
    /ipfs/QmaG4FuMqEBnQNn3C8XJ5bpW8kLs7zq2ZXgHptJHbKDDVx/example.jpg
  
  The chunker option, '-s', specifies the chunking strategy that dictates
  how to break files into blocks. Blocks with same content can
  be deduplicated. The default is a fixed block size of
  256 * 1024 bytes, 'size-262144'. Alternatively, you can use the
  rabin chunker for content defined chunking by specifying
  rabin-[min]-[avg]-[max] (where min/avg/max refer to the resulting
  chunk sizes). Using other chunking strategies will produce
  different hashes for the same file.
  
    > ipfs add --chunker=size-2048 ipfs-logo.svg
    added QmafrLBfzRLV4XSH1XcaMMeaXEUhDJjmtDfsYU95TrWG87 ipfs-logo.svg
    > ipfs add --chunker=rabin-512-1024-2048 ipfs-logo.svg
    added Qmf1hDN65tR55Ubh2RN1FPxr69xq3giVBz1KApsresY8Gn ipfs-logo.svg
  
  You can now check what blocks have been created by:
  
    > ipfs object links QmafrLBfzRLV4XSH1XcaMMeaXEUhDJjmtDfsYU95TrWG87
    QmY6yj1GsermExDXoosVE3aSPxdMNYr6aKuw3nA8LoWPRS 2059
    Qmf7ZQeSxq2fJVJbCmgTrLLVN9tDR9Wy5k75DxQKuz5Gyt 1195
    > ipfs object links Qmf1hDN65tR55Ubh2RN1FPxr69xq3giVBz1KApsresY8Gn
    QmY6yj1GsermExDXoosVE3aSPxdMNYr6aKuw3nA8LoWPRS 2059
    QmerURi9k4XzKCaaPbsK6BL5pMEjF7PGphjDvkkjDtsVf3 868
    QmQB28iwSriSUSMqG2nXDTLtdPHgWb4rebBrU7Q1j4vxPv 338

```

## ipfs files help
```
ipfs filse --help 

>>>>

SUBCOMMANDS
  ipfs files chcid [<path>]      - Change the cid version or hash function of the root node of a given path.
  ipfs files cp <source> <dest>  - Copy files into mfs.
  ipfs files flush [<path>]      - Flush a given path's data to disk.
  ipfs files ls [<path>]         - List directories in the local mutable namespace.
  ipfs files mkdir <path>        - Make directories.
  ipfs files mv <source> <dest>  - Move files.
  ipfs files read <path>         - Read a file in a given mfs.
  ipfs files rm <path>...        - Remove a file.
  ipfs files stat <path>         - Display file status.
  ipfs files write <path> <data> - Write to a mutable file in a given filesystem.
```
