A REST API Server (using Flask) for [PEframe](https://github.com/guelfoweb/peframe), tool to perform static analysis on Portable Executable malware and malicious MS Office documents. This was made to integrate PEframe with [IntelOwl](https://github.com/certego/IntelOwl).

#### DockerHub: https://hub.docker.com/r/eshaan7/peframe-rest-server

## Run Example


```
docker pull eshaan7/peframe-rest-server
docker run -p "4000:4000" -e "WORKERS=1" -e "LOG_LEVEL=INFO" -ti eshaan7/peframe-rest-server
```

## Docker-Compose

There's a `docker-compose.yml` file available in this repo.

```bash
$ docker-compose up
```

## Making calls to API

Creating an analysis request,

```
curl -X POST -F "file=@sample.doc" http://localhost:4000/run_analysis
```

returns JSON,

```
{
   "md5": "19722523ebeefe67aee4bc635c1d5c9",
   "status": "running"
}
```

Then using this hash you can query for the result,

```
curl http://localhost:4000/get_report/19722523ebeefe67aee4bc635c1d5c9
```

Returns result in JSON.