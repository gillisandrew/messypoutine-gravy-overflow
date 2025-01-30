# gravy-overflow

## Install workflow scanning tools

```shell
bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

brew install zizmor
brew install poutine
```

## Scanning

### Run poutine against local repo

```shell
poutine analyze_local . --format sarif > poutine.sarif
```

### Run zizmor against local repo

```shell
zizmor . --pedantic --gh-token "$GITHUB_TOKEN" --output sarif > zizmor.sarif
```

## Reviewing results

### Install SARIF Viewer
```shell
code --install-extension MS-SarifVSCode.sarif-viewer
```

## Tool comparison



| Feature | poutine | zizmor |
|:---- |:------- |:------ |
| extensibility | + written in go with policies defined in rego | - written in rust with custom policy checks |
| useable as github action | + | + |
| updated CVE database | - CVE database embedded at compile-time | + Uses github's CVE database at scan-time |
| tuneable analysis sensitivity | - | + using "personas" |
| outputs findings in standard format | + sarif | + sarif |
| rules are silenceable | ~ per workflow only (config file) | + inline with comment, per workflow, line or line+col (config file)