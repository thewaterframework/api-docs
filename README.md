# api-docs
The science behind the divirod ground sensor network.  


##### File

The ​**file**​ type can constrain the content to send through forms. When this type is used in the context of web forms it SHOULD be represented as a valid file upload in JSON format. File content SHOULD be a base64-encoded string.

| Facet | Description |
|:--------|:------------|
| fileTypes? | A list of valid content-type strings for the file. The file type `*/*` MUST be a valid value.
| minLength? | Specifies the minimum number of bytes for a parameter value. The value MUST be equal to or greater than 0.<br /><br />**Default:** `0`
| maxLength? | Specifies the maximum number of bytes for a parameter value. The value MUST be equal to or greater than 0.<br /><br />**Default:** `2147483647`

```yaml
types:
  userPicture:
    type: file
    fileTypes: ['image/jpeg', 'image/png']
    maxLength: 307200
  customFile:
    type: file
    fileTypes: ['*/*'] # any file type allowed
    maxLength: 1048576
```
