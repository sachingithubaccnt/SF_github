--!jinja2
{% from "regional_macros.jinja" import get_regions %}

{%- set regions = get_regions(DEPLOYMENT_SCOPE).split(",") -%}

{%- for region in regions -%}
  CREATE SCHEMA IF NOT EXISTS {{ region }}_schema;
  USE SCHEMA {{ region }}_schema;
  
  CREATE TABLE {{ region }}_sales_data (
    sale_id NUMBER,
    product_id NUMBER,
    sale_amount FLOAT,
    sale_date DATE
  );
  
  CREATE TABLE {{ region }}_customer_data (
    customer_id NUMBER,
    customer_name VARCHAR,
    region_code VARCHAR
  );
{% endfor %}
