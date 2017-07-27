# To build this Dockerfile:
#
# From the root of configuration:
#
# docker build -f docker/build/e2e/Dockerfile . -t edxops/e2e:latest


FROM edxops/xenial-common:latest
MAINTAINER edxops
USER root
CMD bash -c 'while true; do sleep 60; done'

ENV ACCESS_TOKEN="" \
    BASIC_AUTH_USER="" \
    BASIC_AUTH_PASSWORD="" \
    CONFIG_ROOT="/edx/app/e2e" \
    USER_LOGIN_EMAIL="staff@example.com" \
    USER_LOGIN_PASSWORD="edx" \
    COURSE_ORG="ArbiRaees" \
    COURSE_NUMBER="AR-1000" \
    COURSE_RUN="course" \
    COURSE_DISPLAY_NAME="Manual Smoke Test Course 1 - Auto" \
    EDXAPP_CMS_DOC_LINK_BASE_URL="http://edx.readthedocs.io/projects/open-edx-building-and-running-a-course" \
    GLOBAL_PASSWORD="" \
    LMS_BASE_URL="edx.devstack.lms:18000" \
    LMS_PROTOCOL="http" \
    SELENIUM_BROWSER="chrome" \
    SELENIUM_HOST="edx.devstack.chrome" \
    SELENIUM_PORT="4444" \
    STAFF_USER_EMAIL="" \
    STUDIO_BASE_URL="edx.devstack.studio:18010" \
    STUDIO_PROTOCOL="http" \
    VIRTUAL_ENV="/edx/app/e2e/venvs/e2e"

COPY docker/build/e2e/devstack.sh /edx/app/e2e/

RUN mkdir -p ${CONFIG_ROOT}/venvs \
    && /usr/local/bin/virtualenv ${VIRTUAL_ENV} \
    && . ${VIRTUAL_ENV}/bin/activate \
    && git clone https://github.com/edx/edx-e2e-tests.git ${CONFIG_ROOT}/edx-e2e-tests \
    && cd ${CONFIG_ROOT}/edx-e2e-tests \
    && pip install -r requirements/base.txt \
    && paver install_pages \
    && rm -rf /edx/app/e2e/edx-e2e-tests/ \
    && chmod u+x /edx/app/e2e/devstack.sh
