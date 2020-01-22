ARG BASE_IMAGE=gcr.io/cloud-builders/javac:8
FROM ${BASE_IMAGE}

ARG GRADLE_VERSION=6.0.1
ARG USER_HOME_DIR="/root"
ARG SHA=d364b7098b9f2e58579a3603dc0a12a1991353ac58ed339316e6762b21efba44
ARG BASE_URL=https://services.gradle.org/distributions

ENV GRADLE_HOME "/usr/share/gradle-${GRADLE_VERSION}"
ENV GRADLE_USER_HOME "${USER_HOME_DIR}/.gradle/"

RUN apt-get update -qqy && apt-get install -qqy curl \
  && mkdir -p /usr/share "${GRADLE_USER_HOME}" \
  && curl -fsSL -o "gradle-${GRADLE_VERSION}-bin.zip" "${BASE_URL}/gradle-${GRADLE_VERSION}-bin.zip" \
  && echo "${SHA}  gradle-${GRADLE_VERSION}-bin.zip" | sha256sum -c - \
  && unzip -qq "gradle-${GRADLE_VERSION}-bin.zip" \
  && rm -f "gradle-${GRADLE_VERSION}-bin.zip" \
  && mv "gradle-${GRADLE_VERSION}" /usr/share \
  && ln -s "${GRADLE_HOME}/bin/gradle" /usr/bin/gradle \
  && apt-get remove -qqy --purge curl \
  && rm /var/lib/apt/lists/*_*

ADD gradle.properties "${GRADLE_USER_HOME}"

ENTRYPOINT ["/usr/bin/gradle"]

