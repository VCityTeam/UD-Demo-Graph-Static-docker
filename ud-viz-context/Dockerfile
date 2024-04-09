FROM ubuntu:focal

# Install dependencies
RUN apt-get update
RUN apt-get install -y curl git

# Node version 16 is required. For its installation (on focal) refer to e.g.
#  https://computingforgeeks.com/install-node-js-14-on-ubuntu-debian-linux/
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash - \
 && apt-get install -y nodejs
RUN node --version \
 && npm --version

######### Install UD-Viz demo
WORKDIR /
RUN git clone https://github.com/VCityTeam/UD-Demo-Workspace-GratteCiel.git
WORKDIR /UD-Demo-Workspace-GratteCiel
RUN git checkout 312593c54a1dd591abca169554ed1cfc5614b53d
RUN git submodule init \
 && git submodule update
WORKDIR /UD-Demo-Workspace-GratteCiel/ud-viz-context/UD-Viz
RUN git checkout 6dae5ffe9894cad71321c19dece2dfce0ffd2d13 \
 && npm install
WORKDIR /UD-Demo-Workspace-GratteCiel/ud-viz-context/
COPY bootstrap.js               /UD-Demo-Workspace-GratteCiel/ud-viz-context/src/bootstrap.js
RUN npm install \
 && npm run build
# RUN npm run build-debug

# copy index
COPY index.html                 /UD-Demo-Workspace-GratteCiel/ud-viz-context/index.html
# copy configs
COPY configs/extent_gratteciel.json /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/config/extent_gratteciel.json
COPY configs/frame3D_planars.json   /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/config/frame3D_planars.json
COPY configs/3DTiles.json           /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/config/layer/3DTiles.json
COPY configs/sparql_server.json     /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/config/server/sparql_server.json
COPY configs/help.json              /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/config/widget/help.json
COPY configs/sparql_widget.json     /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/config/widget/sparql_widget.json
# copy html
COPY html/contribute.html           /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/html/contribute.html
COPY html/camera.html               /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/html/camera.html
COPY html/sparql_guide.html         /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/html/sparql_guide.html
COPY html/widget_descriptions.html  /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/html/widget_descriptions.html
# copy queries
COPY queries/buildingCount.rq       /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/queries/buildingCount.rq
COPY queries/buildingsDetails.rq    /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/queries/buildingsDetails.rq
COPY queries/30buildings2009.rq     /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/queries/30buildings2009.rq
COPY queries/30buildings2012.rq     /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/queries/30buildings2012.rq
COPY queries/30buildings2015.rq     /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/queries/30buildings2015.rq
COPY queries/allBuildings2015.rq    /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/queries/allBuildings2015.rq
COPY queries/30buildings2018.rq     /UD-Demo-Workspace-GratteCiel/ud-viz-context/assets/queries/30buildings2018.rq

CMD [ "npm", "run", "start"]
