# WebDAV / HTTP Validation Cheatsheet

## Target

```text
MS2: 192.168.89.128
WebDAV endpoint: /dav/
```

> Use these commands only against the isolated lab target.

## HTTP/WebDAV Discovery

### Inspect endpoint

```bash
curl -i http://192.168.89.128/dav/
```

### Ask the server for supported methods/capabilities

```bash
curl -i -X OPTIONS http://192.168.89.128/dav/
```

Look for:

```text
HTTP/1.1 200 OK
DAV:
Allow:
```

Do not assume the `Allow` header is exhaustive; test the specific method when appropriate.

## WebDAV File Upload

### Create a local test file

```bash
echo "MS2 WebDAV test" > /tmp/webdav-test.txt
```

### Upload with HTTP PUT

```bash
curl -i -T /tmp/webdav-test.txt http://192.168.89.128/dav/webdav-test.txt
```

Useful success response:

```text
201 Created
```

### Retrieve an uploaded file

```bash
curl -i http://192.168.89.128/dav/webdav-test.txt
```

## Harmless PHP Validation

### Create a minimal PHP test

```bash
printf '%s\n' '<?php echo "MS2 PHP TEST"; ?>' > /tmp/webdav-test.php
```

### Upload

```bash
curl -i -T /tmp/webdav-test.php http://192.168.89.128/dav/webdav-test.php
```

### Request

```bash
curl -i http://192.168.89.128/dav/webdav-test.php
```

Interpret the response carefully:

```text
PHP output returned
    → PHP execution confirmed
```

```text
PHP source returned
    → PHP execution not confirmed
```

## Cleanup

```bash
curl -i -X DELETE http://192.168.89.128/dav/webdav-test.txt
```

```bash
curl -i -X DELETE http://192.168.89.128/dav/webdav-test.php
```

## HTTP Status Codes Used in This Lab

| Code | Meaning |
|---|---|
| `200` | OK |
| `201` | Created |
| `404` | Not Found |
| `403` | Forbidden |
| `405` | Method Not Allowed |

## Method Concepts

| Method | Basic purpose |
|---|---|
| `GET` | Retrieve a resource |
| `HEAD` | Retrieve headers without the normal response body |
| `OPTIONS` | Ask about server capabilities |
| `PUT` | Create/replace a resource at a specified URI |
| `DELETE` | Delete a resource |
| `PROPFIND` | WebDAV resource/property discovery |
| `COPY` | Copy a WebDAV resource |
| `MOVE` | Move a WebDAV resource |

## Core Lesson

Do not treat a tool result as the end of the investigation.

A useful validation chain is:

```text
Discovery
   ↓
Capability identification
   ↓
Actual behaviour test
   ↓
Resource creation/access
   ↓
Security-impact validation
   ↓
Cleanup
```
