+++
title = "AWS Lambda with Python"
description = "Scraping Data Feeds"
date = "2018-01-23T12:06:44-05:00"
tags = ["AWS","Python"]
+++

### Update

The bundle of this code is interesting but the bundle is huge! I recommend trying out either of the solutions below.

- [Serverless Framework](https://serverless.com/)
- [AWS Serverless Application Model](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html)


### Intro
[AWS Lambda](https://aws.amazon.com/lambda/) is a hosted platform for running code in the Amazon ecosystem. It supports multiple runtimes including Python! I found that although writing the logic code is easy, there are some unintuitive things that I've stumbled over.

There are three ways you can get your code to Amazon lambda. 

- their inline editor 
- S3://Bucket 
- Zipped up 

The below repo has a preconfigured way to clone a repo, and demonstrate adding packages to run on AWS Lambda quickly.

- 1) Setup an AWS Account and CLI on your machine 
- 2) Provision an AWS Lambda with role `AWSLambdaFullAccess` 
- 3) Create your function with a unique name from the interface



Use the starting point of https://github.com/4projects/python-lambda-template and update `App.py`


### UPDATE CODE 
```
zip -g App.zip *.py
aws lambda update-function-code --function-name $FUNCTION_NAME --zip-file fileb://App.zip
```


**Note** Also update your app handler from `Main.handler` to something like `App.handler`.


## Detailed Writeup

What the application example does in `App.py` does is visits a website, copies down the data (presuming its `json`) and inserts it in DynamoDB. The DynamoDB was also created ahead of time through the AWS interface and an example of this can be used for any json feed.


## Building the bundle

This is how the bundle was built and can be rebuilt. Additional packages can be added in it. 

### Packaging and uploading your bundle

You need to package third-party dependencies. The least painful way is to set up a virtualenv. `pyenv` comes packaged with python3 so after you create a new directory you can do that with:

```
mkdir APP_NAME && cd APP_NAME
python3 -m venv .
```

Then you have to activate your virtual environment. Depending on your terminal pick the appropriate extension.To activate your virtual environment  you would use `bin/activate`. If you're using fish shell, you can use `bin/activate.fish`.

after your `APP_NAME` directory should look like:

```
ls . 
> bin        include    lib        pyvenv.cfg
```

Now install packages to your heart's content. creating a few dependencies or common libs you rely on is wise.

`pip install requests`

Then changing directory to the `site-packages` in your `lib` folder. My directory path happens to be `  $VIRTUAL_ENV/lib/python3.6/site-packages`.

Zip it up `zip -r9 App.zip $VIRTUAL_ENV/lib/python3.6/site-packages`.

