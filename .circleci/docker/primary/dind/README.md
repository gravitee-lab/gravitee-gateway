# How to build

* This OCI image is required to run the circleci pipeline at ccc

* Here is how to buidl and publish this image :

```bash
export DTAG="0.0.2-apim"
export QUAY_BOT_USERNAME=gravitee-lab+graviteebot
export QUAY_BOT_SECRET=VDZBCDFZCDFZCDFZCDFZCDFZCDFZCDFZCDFZCDFZ5ELFI
echo "QUAY_BOT_USERNAME=[$QUAY_BOT_USERNAME]"
echo "QUAY_BOT_SECRET=[${QUAY_BOT_SECRET}]"
git clone	git@github.com:gravitee-lab/gravitee-gateway.git gravitotee/
cd gravitotee/
git checkout feature/add_circleci_yaml
docker build --no-cache -t "quay.io/gravitee-lab/cci-library-dind:${DTAG}" -f .circleci/docker/primary/dind/Dockerfile ./.circleci/docker/primary/dind/
docker login -u="$QUAY_BOT_USERNAME" -p="$QUAY_BOT_SECRET" quay.io
docker push "quay.io/gravitee-lab/cci-library-dind:${DTAG}"
```
