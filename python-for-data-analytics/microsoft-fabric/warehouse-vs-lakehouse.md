---
icon: industry-windows
---

# Warehouse VS Lakehouse

| Features        | Warehouse                                                                  | Lakehouse                                           |
| --------------- | -------------------------------------------------------------------------- | --------------------------------------------------- |
| Definition      | Central repository for structured data optimized for reporting & analytics | Modern architecture combining data lake + warehouse |
| Data Type       | Structured only                                                            | Structured + Semi-structured + Unstructured         |
| Schema          | Schema-on-write                                                            | Schema-on-read + Schema-on-write                    |
| Storage Format  | Proprietary optimized formats                                              | Open formats like Parquet, Delta                    |
| Data Processing | ETL(Extract, Transform, Load)                                              | ELT(Extract, Load, Transform)                       |
| Data Modeling   | Star/Snowflake schema                                                      | Medallion (Bronze, Silver, Gold)                    |
| Tools Examples  | Snowflake, Redshift, Teradata                                              | Databricks, Delta Lake                              |
| Data Quality    | High (clean before load)                                                   | Raw + processed both stored                         |
| Transformation  | Before loading                                                             | After loading                                       |

<figure><img src="../../.gitbook/assets/Media (5).jfif" alt=""><figcaption></figcaption></figure>
