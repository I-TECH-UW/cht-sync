FROM python:3 AS testing

RUN pip install flake8

RUN flake8 dbt-run.py

FROM python:3 AS release

RUN pip install --upgrade cffi \
    && pip install cryptography~=3.4 \
    && pip install dbt-core dbt-postgres

RUN adduser dbt
USER dbt

WORKDIR /dbt/
COPY dbt-run.py dbt-run.py
COPY .dbt .dbt
COPY dbt_project.yml dbt_project.yml
COPY seeds seeds

RUN mkdir old_manifest

CMD ["python3", "/dbt/dbt-run.py"]
