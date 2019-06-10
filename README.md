# Joplin Web : The BackEnd

A Web application for [JoplinApp](https://joplinapp.org)

## why that project ?

Because it may happened we need to access to [JoplinApp](https://joplinapp.org) without having access to his/her smartphone or the Joplin Desktop, and a Web Application could to the trick at a given moment.

## Requirements

* Python >= 3.6
* [Joplin-API](https://github.com/foxmask/joplin-api)
* [starlette](https://starlette.io)

## Installation 

```python
python3 -m venv joplin-web
cd joplin-web
source bin/activate
git clone https://github.com/foxmask/joplin-web
cd joplin-web
pip install -r requirements.txt
```

### settings 

copy env.sample to .env

then set at least this parm: 

* the `JOPLIN_WEBCLIPPER_TOKEN` you have in the Webclipper config page in Joplin
* the `JOPLIN_RESOURCES` to find the files of joplin and being able to load them in the editori 


If you plan to use joplin-terminal and not the WebClipper, in your `.env` file, set `API_USE_JOPLIN_WEBCLIPPER` to `False` then joplin-web will switch of API calls from Rest to command line.


### Running

```python
python app.py &
Joplin Web - Starlette powered
Started server process [10043]
Waiting for application startup.
Uvicorn running on http://0.0.0.0:8001 (Press CTRL+C to quit)
```

Don't forget to start your joplin editor to be able to reach the webclipper port 

## Docker 

if you prefer to use docker instead of using the previous virtualenv, set the paramaters from the ` settings` section above
then

### build

build the image docker
```
docker build -t foxmask/joplin-web .
```

### run

then launch it like this
```
docker run -it --network host -p 8001:8001 --rm --name foxmask-joplin-web-1 foxmask/joplin-web
```

explanations :
 
1) Once the image is built, docker does not even know our local Joplin Webclipper service on the port 41148, so the final trick is to use :
`--network host` which allow docker to access to the network of the host, and here we go.
 
### changing the port 8001 

if you want / need to switch the 8001 for the docker image, you will need to make the following changes :

1) edit the Dockerfile and change 8001 anywhere with your own port
2) change the param `-p` on the `docker run` command 


# Joplin-front : The Frontend

see [`joplin-web/joplin-vue/README.md`](joplin-vue/README.md) file

![Joplin web](https://raw.githubusercontent.com/foxmask/joplin-web/master/joplin_web.png)


