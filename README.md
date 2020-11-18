# Mina Helm Charts

This is an unofficial registry of [Mina](https://minaprotocol.com/) [helm](https://helm.sh/) charts.

## Prerequisites
* [Helm](https://helm.sh/) 3+

## Setup

Add the mina helm repo:
```
helm repo add mina https://k.github.io/mina-helm
helm repo update
```

Then configure a values.yaml for the chart you want to install.

## List of Charts

### [mina](./charts/mina)

Chart to run a Mina Full Node

## Deploy to Github Pages

Deploy requires [`cr`](https://github.com/helm/chart-releaser) tool 

### Enable Github Pages (only first time)

Settings > Options > Github Pages > Source > Select master branch

### Package chart

```
helm package charts/<chart-to-package> --destination .deploy
```

### Upload New Release

```
cr upload --config config.yaml --token <deploy-token>
```

### Generate new index
```
cr index --config config.yaml
git add index.yaml
git commit -m "Update index.yaml"
git push
```

## Build docker images for a testnet

```bash
cd docker/$TESTNET
docker build . -t mina:$TESTNET
docker tag mina:$TESTNET $REGISTRY/mina:$TESTNET
docker push $REGISTRY/mina:$TESTNET
```
