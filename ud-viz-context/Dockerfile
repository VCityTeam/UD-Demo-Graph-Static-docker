FROM ubuntu:focal

# Install dependencies
RUN apt-get update
RUN apt-get install -y \
        curl \
        nodejs \
        git \
 && node --version \
 && npm --version \
 && git --version

# Node version 16 is required. For its installation (on focal) refer to e.g.
#  https://computingforgeeks.com/install-node-js-14-on-ubuntu-debian-linux/
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -

######### Install UD-Viz demo
WORKDIR /
RUN git clone https://github.com/VCityTeam/UD-Demo-Workspace-GratteCiel.git
WORKDIR /UD-Demo-Workspace-GratteCiel
RUN git submodule init \
 && git submodule update
WORKDIR /UD-Demo-Workspace-GratteCiel/ud-viz-context/UD-Viz
RUN git checkout 6bc4b7e25c61d60a46f4d7a0eee19d529e1d1758 \
 && npm install
WORKDIR /UD-Demo-Workspace-GratteCiel/ud-viz-context/
RUN npm install
COPY bootstrap.js /UD-Demo-Workspace-GratteCiel/ud-viz-context/src
COPY config.js /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/

CMD [ "npm", "run", "start"]
