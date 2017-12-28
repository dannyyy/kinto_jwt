# Kinto JWT (Json Web Tokens) authentication policy
This package implements an authentication policy for [Kinto](https://github.com/Kinto/kinto) that using [JSON Web Tokens](https://jwt.io). This standard ([RFC 7519](https://tools.ietf.org/html/rfc7519)) is often used to secure backens APIs. This package is based on the original [pyramid_jwt](https://github.com/wichert/pyramid_jwt) packages with all the necessary adaptions.

## Installation
### Docker
```
docker-compose exec web pip3 install kinto_jwt
```
If this leads to an _access denied_ error try the installation with the additional parameter `--user`

### Regular
```
pip3 install kinto_jwt
```
