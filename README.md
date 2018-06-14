# cf-report-buildpacks

CloudFoundry CLI plugin to find out of date buildpacks in a CloudFoundry installation

## Install from binary

Pick as appropriate for your OS:

```bash
cf install-plugin https://github.com/govau/cf-report-buildpacks/releases/download/v0.1.0/report-buildpacks.linux32
cf install-plugin https://github.com/govau/cf-report-buildpacks/releases/download/v0.1.0/report-buildpacks.linux64
cf install-plugin https://github.com/govau/cf-report-buildpacks/releases/download/v0.1.0/report-buildpacks.osx
cf install-plugin https://github.com/govau/cf-report-buildpacks/releases/download/v0.1.0/report-buildpacks.win32
cf install-plugin https://github.com/govau/cf-report-buildpacks/releases/download/v0.1.0/report-buildpacks.win64
```

## Usage

```bash
cf report-buildpacks
```

## Development

```bash
dep ensure
go install ./cmd/report-buildpacks && \
    cf install-plugin $GOPATH/bin/report-buildpacks -f && \
    cf report-buildpacks
```

## Building a new release

```bash
PLUGIN_PATH=$GOPATH/src/github.com/govau/cf-report-buildpacks/cmd/report-buildpacks
PLUGIN_NAME=$(basename $PLUGIN_PATH)

GOOS=linux GOARCH=amd64 go build -o ${PLUGIN_NAME}.linux64 cmd/${PLUGIN_NAME}/${PLUGIN_NAME}.go
GOOS=linux GOARCH=386 go build -o ${PLUGIN_NAME}.linux32 cmd/${PLUGIN_NAME}/${PLUGIN_NAME}.go
GOOS=windows GOARCH=amd64 go build -o ${PLUGIN_NAME}.win64 cmd/${PLUGIN_NAME}/${PLUGIN_NAME}.go
GOOS=windows GOARCH=386 go build -o ${PLUGIN_NAME}.win32 cmd/${PLUGIN_NAME}/${PLUGIN_NAME}.go
GOOS=darwin GOARCH=amd64 go build -o ${PLUGIN_NAME}.osx cmd/${PLUGIN_NAME}/${PLUGIN_NAME}.go

shasum -a 1 ${PLUGIN_NAME}.*
```
