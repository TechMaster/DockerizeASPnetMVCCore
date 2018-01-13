
```docker
docker build -t himvc .
docker run -d -p 80:5000 himvc:latest
curl http://localhost
```