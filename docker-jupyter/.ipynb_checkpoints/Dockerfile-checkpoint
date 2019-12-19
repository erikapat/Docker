# our base image
FROM python:3-onbuild


#create an src working directory and copy the entire directory over to it—data, notebook, and all. Once it is started, the container will have an exact copy of what you have locally.
RUN mkdir src
WORKDIR src/
COPY . .

RUN pip3 install -r requirements.txt
RUN pip3 install jupyter

RUN python3 module.py

#RUN rm /src/data/raw_data.csv
#WORKDIR /src/notebooks
WORKDIR notebooks

# Add Tini. Tini operates as a process subreaper for jupyter. This prevents kernel crashes.
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
