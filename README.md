How to reproduce this lambda deployment package
======================================================================
NOTE: The following instructions are tested in Cloud9 with Amazon Linux 2023 AMI


cd into project dir
create lambda_function.py

python3 -m venv thumbnail_venv
source ./thumbnail_venv/bin/activate

python3 -m pip install --upgrade pip

pip install boto3
pip install pillow

deactivate

NOTE: Remember to replace python version to the current one

cd thumbnail_venv/lib/python3.9/site-packages

zip -r ../../../../lambda_python_thumbnail_deployment_package.zip .

cd ../../../../

zip lambda_python_thumbnail_deployment_package.zip lambda_function.py

NOTE: Use the same python version as the development one when creating the lambda function.

aws lambda create-function --function-name Thumbnail-venv --zip-file fileb://lambda_python_thumbnail_deployment_package.zip --handler lambda_function.lambda_handler --runtime python3.9 --timeout 10 --memory-size 1024 --role arn:aws:iam::000000000000:role/Lambda-Load-Inventory-Role --region us-east-1

References:
https://docs.aws.amazon.com/lambda/latest/dg/with-s3-tutorial.html#with-s3-tutorial-create-function-package
https://docs.aws.amazon.com/lambda/latest/dg/python-package.html#python-package-create-dependencies

External python package layers
https://github.com/keithrozario/Klayers
