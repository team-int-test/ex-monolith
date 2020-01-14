FROM python:3
#
# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive
#
COPY requirements.txt .
COPY application.py .
#
# Configure apt and install packages
RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
    #
    # Verify git, process tools, lsb-release (common in install instructions for CLIs) installed
    && apt-get -y install git iproute2 procps lsb-release \
    #
    && pip --disable-pip-version-check --no-cache-dir install -r requirements.txt \
    #
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*
#
# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=dialog
EXPOSE 5050
#
#
CMD [ "python", "./application.py" ]