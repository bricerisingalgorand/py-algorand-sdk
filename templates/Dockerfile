# This Dockerfile is based on the example automation Dockerfile available here:
# https://github.com/algorand/generator/blob/master/examples/repo_template_dir/Dockerfile

# ==============================
# > BUILD AND GENERATE
# ==============================

FROM algorand-generator as generator

# ==============================
# > FORMAT
# ==============================

FROM python:3.7.9 as formatter

# Copy files from previous build stage
COPY --from=generator /repo /repo
WORKDIR /repo

# SDK dependencies, and source version of behave with tag expression support
RUN pip install . -q \
    && pip install git+https://github.com/behave/behave -q

# Format generated code
# RUN make format

# ==============================
# > PUBLISH
# ==============================

FROM generator as publisher

# Copy work directory from previous stage to the /repo directory
COPY --from=formatter /repo /repo