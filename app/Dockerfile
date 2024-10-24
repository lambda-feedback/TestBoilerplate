# Base image that bundles AWS Lambda Python 3.11 image with some middleware functions
# FROM base-eval-tmp
FROM ghcr.io/lambda-feedback/baseevalutionfunctionlayer:pr-13-3.11
# FROM ghcr.io/lambda-feedback/baseevalutionfunctionlayer:3.11  #- relative import error
# FROM rabidsheep55/python-base-eval-layer                      #- python 3.8

# Copy and install any packages/modules needed for your evaluation script.
COPY requirements.txt ${LAMBDA_TASK_ROOT}
RUN pip3 install -r ${LAMBDA_TASK_ROOT}/requirements.txt

# Copy the evaluation and testing scripts
COPY evaluation.py ./app/
COPY evaluation_tests.py ./app/

# Copy the preview and testing scripts
COPY preview.py ${LAMBDA_TASK_ROOT}/app/
COPY preview_tests.py ${LAMBDA_TASK_ROOT}/app/

# Copy Documentation
COPY docs/dev.md ${LAMBDA_TASK_ROOT}/app/docs/dev.md
COPY docs/user.md ${LAMBDA_TASK_ROOT}/app/docs/user.md

# Set permissions so files and directories can be accessed on AWS
RUN chmod 644 $(find . -type f)
RUN chmod 755 $(find . -type d)

# The entrypoint for AWS is to invoke the handler function within the app package
CMD [ "app.handler.handler" ]
