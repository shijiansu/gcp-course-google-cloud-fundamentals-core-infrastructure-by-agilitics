
```shell
git clone https://github.com/GoogleCloudPlatform/appengine-guestbook-python
cd appengine-guestbook-python
ls -l
cat app.yaml
# Run the application using the built-in App Engine development server
dev_appserver.py ./app.yaml
## Preview on port 8080

# run at App Engine
gcloud app deploy ./index.yaml ./app.yaml
```
