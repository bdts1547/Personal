# CAP JAVA


##### Change default URL in application:
In file srv/src/main/resources/application.yaml:

```
...
cds:
  odata-v4.endpoint.path: "/api"
```
In catalogService:
```
@path : 'browse'
service CatalogService {
  entity Books as projection on bookshop.Books;
}
```