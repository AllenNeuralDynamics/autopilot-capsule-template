# hash:sha256:ea4b2c4bbb4393490a8b3fe06abcd1812e343c8bab72957809440268577bc55d
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/python-slim-uv:main-5692e50

ARG DEBIAN_FRONTEND=noninteractive
ARG GIT_ASKPASS
COPY git-ask-pass /

COPY postInstall /
RUN --mount=type=secret,id=secrets . /run/secrets/secrets \
    && /postInstall
