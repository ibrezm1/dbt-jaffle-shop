## dbt quick setup on local
```bash
$ python3 -m venv dbt-env 
$ source dbt-env/bin/activate
$ pip3 install --upgrade dbt-bigquery
$ dbt init first_project
$ cd first_project/
$ dbt debug --profiles-dir .    # dbt debug if local profiles then setup env variable 
$ export DBT_PROFILES_DIR=$(pwd)
$ dbt run    # Will not work ... set up 
$ vim ~/.dbt/profiles.yml
$ gcloud auth application-default login  # Set up oauth used here
$ dbt docs generate
$ dbt docs serve  # Local host docs
```
* Best to set up configurations in gcloud [GCP configurations setup](https://medium.com/google-cloud/how-to-use-multiple-accounts-with-gcloud-848fdb53a39a)
* Switch to new configuration [Switching configs](https://stackoverflow.com/questions/35744901/how-to-change-the-active-configuration-profile-in-gcloud)
* Auth login [Auth login in gcp](https://stackoverflow.com/questions/67608814/how-to-switch-gcp-authentication-account-for-dbt-bigquery-runs)
* Fillipe holla Setup [dbt-setup](https://hoffa.medium.com/get-started-with-bigquery-and-dbt-the-easy-way-36b9d9735e35)
* Demo Model setup [springml](https://www.springml.com/blog/getting-started-with-data-build-tool-dbt-for-bigquery/)
* Original github [here](https://github.com/sungchun12/dbt_bigquery_example)
* Static page on gcp [GCS](https://cloud.google.com/storage/docs/hosting-static-website#storage-create-bucket-gsutil)
* dbt same example [here](https://docs.getdbt.com/tutorial/create-a-project-dbt-cli)
* dbt full usage in project [here](https://engineering.mercari.com/en/blog/entry/20201207-toward-better-data-management-on-bigquery-with-dbt/)
* dbt sheduled queries update [here](https://blog.redpillanalytics.com/how-dbt-was-used-to-convert-from-google-bigquery-scheduled-queries-8f909be12fcc)

## Testing dbt project: `jaffle_shop`

`jaffle_shop` is a fictional ecommerce store. This dbt project transforms raw data from an app database into a customers and orders model ready for analytics.

### What is this repo?
What this repo _is_:
- A self-contained playground dbt project, useful for testing out scripts, and communicating some of the core dbt concepts.

What this repo _is not_:
- A tutorial — check out the [Getting Started Tutorial](https://docs.getdbt.com/tutorial/setting-up) for that. Notably, this repo contains some anti-patterns to make it self-contained, namely the use of seeds instead of sources.
- A demonstration of best practices — check out the [dbt Learn Demo](https://github.com/dbt-labs/dbt-learn-demo) repo instead. We want to keep this project as simple as possible. As such, we chose not to implement:
    - our standard file naming patterns (which make more sense on larger projects, rather than this five-model project)
    - a pull request flow
    - CI/CD integrations
- A demonstration of using dbt for a high-complex project, or a demo of advanced features (e.g. macros, packages, hooks, operations) — we're just trying to keep things simple here!

### What's in this repo?
This repo contains [seeds](https://docs.getdbt.com/docs/building-a-dbt-project/seeds) that includes some (fake) raw data from a fictional app.

The raw data consists of customers, orders, and payments, with the following entity-relationship diagram:

![Jaffle Shop ERD](/etc/jaffle_shop_erd.png)


### Running this project
To get up and running with this project:
1. Install dbt using [these instructions](https://docs.getdbt.com/docs/installation).

2. Clone this repository.

3. Change into the `jaffle_shop` directory from the command line:
```bash
$ cd jaffle_shop
```

4. Set up a profile called `jaffle_shop` to connect to a data warehouse by following [these instructions](https://docs.getdbt.com/docs/configure-your-profile). If you have access to a data warehouse, you can use those credentials – we recommend setting your [target schema](https://docs.getdbt.com/docs/configure-your-profile#section-populating-your-profile) to be a new schema (dbt will create the schema for you, as long as you have the right privileges). If you don't have access to an existing data warehouse, you can also setup a local postgres database and connect to it in your profile.

5. Ensure your profile is setup correctly from the command line:
```bash
$ dbt debug
```

6. Load the CSVs with the demo data set. This materializes the CSVs as tables in your target schema. Note that a typical dbt project **does not require this step** since dbt assumes your raw data is already in your warehouse.
```bash
$ dbt seed
```

7. Run the models:
```bash
$ dbt run
```

> **NOTE:** If this steps fails, it might mean that you need to make small changes to the SQL in the models folder to adjust for the flavor of SQL of your target database. Definitely consider this if you are using a community-contributed adapter.

8. Test the output of the models:
```bash
$ dbt test
```

9. Generate documentation for the project:
```bash
$ dbt docs generate
```

10. View the documentation for the project:
```bash
$ dbt docs serve
```

### What is a jaffle?
A jaffle is a toasted sandwich with crimped, sealed edges. Invented in Bondi in 1949, the humble jaffle is an Australian classic. The sealed edges allow jaffle-eaters to enjoy liquid fillings inside the sandwich, which reach temperatures close to the core of the earth during cooking. Often consumed at home after a night out, the most classic filling is tinned spaghetti, while my personal favourite is leftover beef stew with melted cheese.

---
For more information on dbt:
- Read the [introduction to dbt](https://docs.getdbt.com/docs/introduction).
- Read the [dbt viewpoint](https://docs.getdbt.com/docs/about/viewpoint).
- Join the [dbt community](http://community.getdbt.com/).
---
