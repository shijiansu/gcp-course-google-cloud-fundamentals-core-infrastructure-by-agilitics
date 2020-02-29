
```shell
# startup script
apt-get update
apt-get install apache2 php php-mysql -y
service apache2 restart
```

```shell
# For convenience, enter your chosen location into an environment variable called LOCATION. Enter one of these commands:
export LOCATION=US
# Or
export LOCATION=EU
# Or
export LOCATION=ASIA

# In Cloud Shell, the DEVSHELL_PROJECT_ID environment variable contains your project ID. Enter this command to make a bucket named after your project ID:
gsutil mb -l $LOCATION gs://$DEVSHELL_PROJECT_ID
# Retrieve a banner image from a publicly accessible Cloud Storage location:
gsutil cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png
# Copy the banner image to your newly created Cloud Storage bucket:
gsutil cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png
# Modify the Access Control List of the object you just created so that it is readable by everyone:
gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png
```

```shell
# sudo nano index.php
# ctrl + o -> save
# ctrl + x -> exit
sudo service apache2 restart
```
