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

## Settings
The settings can be done inside the `kinto.ini` configuration file.

### Example
```
multiauth.policies = kinto_jwt
multiauth.policy.kinto_jwt.use = kinto_jwt.JWTAuthenticationPolicy
multiauth.policy.kinto_jwt.public_key = -----BEGIN PUBLIC KEY-----
	MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsYwmKeF5DHuWpz8+dG9M
	xdg/SRwGb37zkBM6LJPwbLdvCgOm4aYfh5I3Gz5kZVh4wqcxoM+BRAo6HG5xek5p
	VBAJ1S9rRieGBGoaAdTRlIh45xBeSthPOx1fZVQIDUf16tQPhG4PhAnkgWDDMFV8
	crXfv8oFT7PJeb0ZLYUEviwqqKdqzyT2Ztdo0k49kOYrTJBvmUXADGEEIt7TeAIY
	FAWA9Z7fOD+Euh/PgihJc4HM39n/rxvZvlQ8dkEBheIzRyrLMIxkD5mxQXNd/Hte
	IabcwU9bcsRmje06vWgmYCaWakkJh6EnhDXG7mmgE/KeO1em3ZHWy95BSBmI5+hJ
	eQIDAQAB
	-----END PUBLIC KEY-----
multiauth.policy.kinto_jwt.algorithm = RS256
multiauth.policy.kinto_jwt.audience = LHVRVt7MxVY90i1BpRdZzd6Mh8z88vq2
multiauth.policy.kinto_jwt.unauthorizedUserId = public
multiauth.policy.kinto_jwt.userIdTokenKey = sub
```

### Parameters
| Parameter | Ini-file entry | Default | Description |
| --------- | -------------- | ------- | ----------- |
| public_key | kinto_jwt.public_key | | Key used to verify token signature. For asymetric keys (RSA) the private key is expected not the full certificate. For HMAC based tokens the secret is expected |
| algorithm | kinto_jwt.algorithm | RS256 | Encryption (RSA) or hashing (HMAC) algorithm |
| leeway | kinto_jwt.leeway | 0 | Number of seconds a token is allowed to be expired before it is rejected |
| http_header | kinto_jwt.http_header | Authorization | HTTP header used for the token |
| auth_type | kinto_jwt.auth_type | JWT | Authentication type used in the authentication header (e.g. JWT or Bearer). |
| audience | kinto_jwt.audience | | If the token is issued with an audience the value must be specified |
| verifyToken | kinto_jwt.verifyToken | True | Should only be deactived for development purposes |
| unauthorizedUserId | kinto_jwt.unauthorizedUserId | public | The userId which should be returned for invalid authentication requests |
| userIdTokenKey | kinto_jwt.userIdTokenKey | sub | The key of the JWT (Json Web Token) which includes the userId |
