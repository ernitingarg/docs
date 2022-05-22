### IPFS commands

```
ipfs init # connect to network
ipfs add # To add
ipfs cat # To display
ipfs get # To download 
ipfs add -w # To add more directory information eg: size, Name.
ipfs add -r # To add recursively
ipfs ls -v # display more directory information eg: size, Name.
ipfs pin ls # To list pinned items
ipfs pin # To pin
ipfs object get # To get CIDs structure (chunks)

# Examples:
ipfs cat /ipfs/Qmd286K6pohQcTKYqnS1YhWrCiS4gz7Xi34sdwMe9USZ7u/readme
ipfs cat /ipfs/Qmd286K6pohQcTKYqnS1YhWrCiS4gz7Xi34sdwMe9USZ7u/cat.jpg > cat.jpg
ipfs add index.html
ipfs cat /ipfs/<cid>
ipfs add -r dir
ipfs object get Qmd286K6pohQcTKYqnS1YhWrCiS4gz7Xi34sdwMe9USZ7u
ipfs object get Qmd286K6pohQcTKYqnS1YhWrCiS4gz7Xi34sdwMe9USZ7u | jq
ipfs cat Qmd286K6pohQcTKYqnS1YhWrCiS4gz7Xi34sdwMe9USZ7u > nature.jpg
```

## IPFS Online
```
ipfs daemon & # Participate to IPFS network
ipfs id # To get local node id
ipfs swarn peers # List all peers connected to

# Local node
localhost:8080/ipfs/cid
localhost:8080/ipns/cid

# Public gateway (offical one)
ipfs.io/ipfs/cid

# Other ones
cloudflare-ipfs/ipfs/cid
siderus.io/ipfs/cid

# Node status, network traffic, peers etc
localhost::5001/webui 
```

## Mutable Links with IPNS
```
ipfs key gen --type=rsa --size=2048 test
ipfs key list
ipfs namne publish --key=test cid1
ipfs.io/ipns/key_cid
ipfs namne publish --key=test cid2
```

## Brave Browser
```
ipfs://<cid>
```

