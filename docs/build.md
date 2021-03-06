# Build Mining Pool

## Requirements

* Windows: dotNet v4.5+.
* Linux: mono v3.2+.
Install the latest version from:
https://www.mono-project.com/download/stable/#download-lin
* MacOS over mono v3.2+.

## Steps to Build

1. Clone the repository
```
git clone https://github.com/WillyTheCat/bitcashpool
```
2. Change directory to the project root
```
cd bitcashpool
```
3. Install dependencies

If you do not have nuget already, install nuget:
```
sudo apt-get install nuget
```
Then install the dependencies
```
nuget restore
```
4. Build from sources
```
xbuild CoiniumServ.sln /p:Configuration="Debug"
# or
xbuild CoiniumServ.sln /p:Configuration="Release"
```

Last command create binaries in `build/bin/Debug` or `build/bin/Relese` folders.
