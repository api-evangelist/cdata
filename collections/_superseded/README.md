# Superseded collections

These Postman and OpenCollection files were generated from the doc-derived OpenAPI
definitions now archived in `openapi/_original/superseded/`. They encode metadata paths
(`/catalogs/{catalog}/schemas`, `/catalogs/{catalog}/schemas/{schema}/tables`) that CData's
real REST API does not serve — the published contract uses flat `/schemas`, `/tables` and
`/columns` with query parameters.

They are moved here rather than deleted so the provenance trail survives. New collections
should be generated from the first-party specs harvested on 2026-09-05 and registered in
`apis.yml` (`openapi/cdata-rest-api-openapi.yml`, `openapi/cdata-management-api-openapi.yml`
and the rest).
