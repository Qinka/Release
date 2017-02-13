Glob 0.1.0-rc(3)(0.1.0.50)
===

A more stable glob version for preview. 

* Authentication via RSA Public/Private Key

## Download && Usage

Pull the image from docker
```shell
docker pull qinka/glob:glob-0.1.0-docker-0.1.0-rc1-8b82f93-Linux-Ubuntu-trusty-GHC_8.0.2-x86_64-threaded
```
or
```shell
docker pull qinka/glob:glob-0.1.0-docker-0.1.0-rc1-8b82f93-Linux-Ubuntu-trusty-GHC_8.0.2-x86_64-llvm-3.7-threaded
```

You can also download the files:
[glob-0.1.0.bin.x86_64.docker.linux.llvm-3.7.tar.xz](http://prj.qinka.pw/release/release/glob/v0.1.0-rc.3/glob-0.1.0.bin.x86_64.docker.linux.llvm-3.7.tar.xz)
or 
[glob-0.1.0.bin.x86_64.docker.linux.tar.xz](http://prj.qinka.pw/release/release/glob/v0.1.0-rc.3/glob-0.1.0.bin.x86_64.docker.linux.tar.xz)
And use `docker load` load the images.

If your want to see ugly man page, you can download 
[glob-doc-0.1.0-wiki.tar.xz](http://prj.qinka.pw/release/release/glob/v0.1.0-rc.3/glob-doc-0.1.0-wiki.tar.xz),
and run:
```shell
make install
```

If you want to get the codes, download [source code(tar.gz)](https://github.com/Qinka/Glob/archive/v0.1.0-rc.3.tar.gz), or
[source code(zip)](https://github.com/Qinka/Glob/archive/v0.1.0-rc.3.zip).
And you can also using git:
```shell
git clone https://github.com/Qinka/Glob.git
git checkout v0.1.0-rc.3
```
And if you want the latest one, checkout to the `master` or development branch.

## Build && Tools

Using stack to build these things.
```bash
stack build glob-launch # build glob-launch
stack build glob-update # build glob-update, a tool to help upload and update
stack build glob-ih     # build glob-ih, a tool to help identify
stack build glob-timecheck # build glob-timecheck, a tool to check the delay between the backend and your computer.
```

If you want to create the public and private key, you need load a haskell's ghc docker-image, then save the following to `MkKey.hs`
```haskell
#!runghc
import Crypto.PubKey.RSA

fileName :: String
fileName = undefined   -- need to change

size :: Int
size = undefined       -- need to change
e :: Integer
e = undefined          -- need to change

main :: IO ()
main = do
  (pub,pri) <- generate size e
  writeFile (fileName++".pub") $ show pub
  writeFile fileName $ show private
```
and change the `fileName`, `size`, and `e`, and run:
```bash
cabal install cryptonite
chmod a+x MkKey.hs
./MkKey.hs
```

