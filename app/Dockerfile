# Base image that bundles AWS Lambda Python 3.11 image with some middleware functions
# FROM base-eval-tmp
# FROM ghcr.io/lambda-feedback/baseevalutionfunctionlayer:pr-13-3.11
# FROM ghcr.io/lambda-feedback/baseevalutionfunctionlayer:3.11  # - relative import error
FROM ghcr.io/lambda-feedback/baseevalutionfunctionlayer:main-3.8
# FROM rabidsheep55/python-base-eval-layer                      

WORKDIR /app

# Copy and install any packages/modules needed for your evaluation script.
COPY requirements.txt .
RUN pip3 install -r requirements.txt

# Copy the evaluation and testing scripts
COPY evaluation.py ./app/
COPY evaluation_tests.py ./app/

# Copy the preview and testing scripts
COPY preview.py ./app/
COPY preview_tests.py ./app/

# Copy Documentation
COPY docs/dev.md ./app/docs/dev.md
COPY docs/user.md ./app/docs/user.md

# Set permissions so files and directories can be accessed on AWS
RUN chmod 644 $(find . -type f)
RUN chmod 755 $(find . -type d)

# The entrypoint for AWS is to invoke the handler function within the app package
# ENTRYPOINT ["/usr/local/bin/aws-lambda-rie", "/var/runtime/bootstrap"]

# ENV PYTHONPATH="/"

CMD ["/app/app.handler"]