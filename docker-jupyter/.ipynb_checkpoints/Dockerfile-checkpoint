# our base image
FROM python:3-onbuild


#create an src working directory and copy the entire directory over to it—data, notebook, and all. Once it is started, the container will have an exact copy of what you have locally.
RUN mkdir src
WORKDIR src/
COPY . .

RUN pip3 install -r requirements.txt
RUN pip3 install jupyter

RUN python3 module.py
RUN rm /src/data/raw_data.csv
WORKDIR /src/notebooks

#RUN jupyter notebook --generate-config
#RUN echo "c.NotebookApp.password='sha1:f238bbafb661:88e7cda084cc30fcce5e93f22226401590545804'">>/root/.jupyter/jupyter_notebook_config.py

CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
