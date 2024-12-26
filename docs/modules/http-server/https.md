# HTTPS

You need to have OpenSSL installed.

Then run:

```bash
openssl genpkey -algorithm RSA -out ./tmp/private-key.pem 
openssl req -new -key ./tmp/private-key.pem -out ./tmp/csr.pem
openssl x509 -req -days 365 -in ./tmp/csr.pem -signkey ./tmp/private-key.pem -out ./tmp/certificate.pem
```

Cf. [A Detailed look into the Node.js HTTP module, by Mirza Leka](https://mirzaleka.medium.com/a-detailed-look-into-the-node-js-http-module-680eb5e4548a#b963).

Then put your private key file's and certificate file's paths in your http config file.

```ts
    // ...

    https: {
        key: 'tmp/private-key.pem',
        cert: 'tmp/certificate.pem',
    },

    // ...
```

The project will start two servers, the one on HTTPS and the second in HTTP that will do the redirections to the HTTPS one.
