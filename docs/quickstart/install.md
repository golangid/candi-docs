# Install CLI
**For linux:**
```
$ wget -O candi https://storage.googleapis.com/agungdp/bin/candi/candi-linux && chmod +x candi && sudo mv candi /usr/local/bin
$ candi
```

**For macOS:**
```
$ wget -O candi https://storage.googleapis.com/agungdp/bin/candi/candi-osx && chmod +x candi && mv candi /usr/local/bin
$ candi
```

**For windows:**
```
https://storage.googleapis.com/agungdp/bin/candi/candi-x64.exe (64 bit)
or 
https://storage.googleapis.com/agungdp/bin/candi/candi-x86.exe (32 bit)
```

**Or build binary from source:**
```
$ go install github.com/Bhinneka/candi/cmd/candi@latest
$ candi
```

**Flag options:**
```
$ candi --help
Usage of candi:
  -add-handler
        [project generator] add handler in delivery module in service
  -add-module
        [project generator] add module in service
  -init
        [project generator] init service
  -init-monorepo
        [project generator] init monorepo codebase
  -libraryname string
        [project generator] define library name (default "github.com/Bhinneka/candi"), you can custom set to CANDI_CLI_PACKAGES global environment variable 
  -monorepo-name string
        [project generator] set monorepo project name (default "monorepo")
  -output string
        [project generator] directory to write project to (default is service name)
  -packageprefix string
        [project generator] define package prefix
  -protooutputpkg string
        [project generator] define generated proto output target (if using grpc), with prefix is your go.mod
  -run
        [service runner] run selected service or all service in monorepo
  -scope string
        [project generator] set scope 
        1 for init service, 
        2 for add module(s), 
        3 for add delivery handler(s) in module, 
        4 for init monorepo codebase, 
        5 for run multiple service in monorepo
  -service string
        Describe service name (if run multiple services, separate by comma)
  -version
        print version
  -withgomod
        [project generator] generate go.mod or not (default true)
```

## Generating Project
<a href="#/quickstart/monorepo">Click Here For Monorepo</a>

<a href="#/quickstart/microservice">Click Here For Microservice</a>