> Sources:
> https://medium.com/better-programming/how-to-create-ssl-certificates-for-development-861237235933
> https://deliciousbrains.com/ssl-certificate-authority-for-local-https-development/
> https://letsencrypt.org/docs/certificates-for-localhost/
> https://docs.master.dockerproject.org/engine/security/https/

# Theory

## Definition

SSL is `Secure Socket Layer` which is the base of the new protocol known as TLS which stands for `Transport Layer Security`, So when people say SSL they usually referring to TLS instead.

They are PKI protocols `Public Key Infrastructure` which is based on Public Key Cryptography know for it's key pair `Public & Private`.

# Generating Local SSL Certs

## Tutorial By Medium

### Without CA

In order to generate an ssl certificate these steps must be honored in the following order

1. Generating Private Key
2. Creating Certificate Signing Request
3. Generating the Certificate

#### Generating Private Key

```bash
openssl genpkey -algorithm rsa -des3 -out private_key.pem -pkeyopt rsa_keygen_bits:4096
```

```
openssl                     # full fledged cryptographic libray
genpkey                     # generate private key

-algorithm                  # which algorithm to use
    rsa                         # use RSA (Raivest-Shamire-Adelman)

-des3                       # encrypt the generated private key with DES3

-out                        # output the private key in PKCS#8 format to a file named
    private_key.pem         # this name

-pkeyopt                    # private key options
    rsa_keygen_bits:        # RSA bit length
        4096                # 4096 bits long
```

> Warning: using `genpkey` is required since `genrsa` uses `512` bits default key length with is really weak.


#### Creating Certificate Signing Request (CSR)

This is like an order to ask for a certificate, This is usually sent to a trusted Certificate Authority `CA`; But since we're the `CA` we will self generate and sign our own certificates.

The most important thing to keep in mind is that `openssl` will ask multiple questions in order to "fill" the certificate fields with. One of these questions is the `Common Name` or `CN` which is important since it should be a `Fully Qualified Domain Name` aka `FQDN` it cloud be **public** or **private** domain and even `localhost` or an `IP Address`.

> Note : Chromium no longer trusts `CN` use `SAN` instead

```bash
openssl req -new -key private_key.pem -out csr.pem
```

```
req                         # create a certificate request in PKCS#10 format
-new                        # it will be a new one so ask all the questions
-key                        # with the private key named
    private_key.pem
-out                        # output it to a file named
    csr.pem                 # this name
```

Then the following questions will be asked

- Fully Qualified Domain Name (FQDN)
- Organization
- Organization Unit (OU)
- City or locality
- State or province
- Country


#### Generating The Certificate

This part explains why this is a self signed certificate since this is usually done by a trusted CA's private key where it sign your certificate so that it's trusted by all systems that trust this CA. However in this case we're the CA so we'll sign it our selves.

```bash
openssl x509 -in csr.pem -out certificate.pem -req -signkey private_key.pem -days 365
```

```
x509                        # certification command

-req                        # the input file is a CSR

-in                         # take a file named
    csr.pem                 # this name

-out                        # output a certificate named
    certificate.pem         # this name

-signkey                    # use the following private key to sing the certificate
    private_key.pem         # this private key

-days                       # certificate expires after the following number of days
    365                     # 365
```

### With CA

- Generating CA's Private Key
- Generating Root Certificate
- Creating Private Key For The Client Certificate
- Creating Client Certificate Signing Request (CSR)
- Creating Client Certificates Signed By CA's Private Key

#### Generating The CA's Private Key

```bash
openssl genpkey -algorithm rsa -des3 -out private_key_ca.pem -pkeyopt rsa_keygen_bits:4096
```

Check out the command explanation in the previous section.

#### Generating Root Certificate

The CA's root certificate is the one that is going to be in your OS or Web Browser's trusted certificates to be checked against

```bash
openssl req -x509 -new -key private_key_ca.pem -sha256 -days 365 -out ca_certificate.pem
```

The information you fill in in this one isn't really that important, just put information that enables you to distinguish it from other certificates.

#### Creating Private Key For The Certificate

```bash
opensll genpkey -algorithm rsa -des3 -out private_key.pem -pkeyopt rsa_keygen_bits:4096
```

#### Creating Certificate Signing Request (CSR)

```bash
openssl req -new -key private_key.pem -out csr.pem
```

Again openssl will ask multiple questions, the most important one is the `Common Name` or `CN` it could be also `Subject Alternative Name` aka `SAN` just put your `FQDN` or `IP Address`.

#### Creating Certificate Signed By CA's Private Key

```bash
openssl x509 -req -in csr.pem -CA ca_certificate.pem -CAkey private_key_ca.pem -CAcreateserial -out certificate.crt -days 365
```

```
-CA                             # use CA certificate named
    ca_certificate.pem          # this name
-CAkey                          # use CA private key named
    private_key_ca.pem          # this name
-CAcreateserial                 # create certificate serial number
```

## Tutorial By Let's Encrypt

```bash
openssl req -x509 -out localhost.crt -keyout localhost.key \
  -newkey rsa:2048 -nodes -sha256 \
  -subj '/CN=localhost' -extensions EXT -config <( \
   printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```

## Tutorial By DeliciousBrains

- Generating CA's Private Key
- Generating CA's root Certificate

### Generating CA's private key

```bash
openssl genrsa -des3 -out myCA.key 2048
```

### Generating CA's CSR & Root Certificate

```
openssl req -x509 -new -nodes -key myCA.key -sha256 -days 1825 -out myCA.pem
```

You'll be asked a few questions the most important ones are the `Common Name` & `Subject Alternative Name` or `CN` and `SAN` respectively. They represent the same thing, so depending on the web browser you're using `CN` or `SAN` might be checked. Fill these options with your `FQDN` or `IP Address`.

After generating the CA's root certificate added it to your devices and browsers that are going to be accessing your HTTPS web sites or services.

### Creating Certificates For Your Services

Generating the private key for that service so that we can create a CSR

```bash
openssl genrsa -out dev.deliciousbrains.key 2048
```

Creating a Certificate Signing Request

```bash
openssl req -new -key dev.deliciousbrains.key -out dev.deliciousbrains.csr
```

The same questions are going to appear make sure to put the right `CN` & `SAN`.

Create a file named `dev.deliciousbrains.ext` with this content

```
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = dev.deliciousbrains.com
```

Then generate the certificate with

```bash
openssl x509 -req -in dev.deliciousbrains.csr -CA myCA.pem -CAkey myCA.key -CAcreateserial \
    -out dev.deliciousbrains.crt -days 825 -sha256 -extfile dev.deliciousbrains.ext
```

## Tutorial by docker

```bash
openssl genrsa -aes256 -out ca-key.pem 4096
```

```bash
openssl req -new -x509 -days 365 -key ca-key.pem -sha256 -out ca.pem
```

Now that you have a CA, you can create a server key and certificate signing request (CSR). Make sure that “Common Name” matches the hostname you use to connect to Docker:

```bash
openssl genrsa -out server-key.pem 4096
```

```bash
openssl req -subj "/CN=$HOST" -sha256 -new -key server-key.pem -out server.csr
```

Next, we’re going to sign the public key with our CA:

Since TLS connections can be made through IP address as well as DNS name, the IP addresses need to be specified when creating the certificate. For example, to allow connections using 10.10.10.20 and 127.0.0.1:

```bash
echo subjectAltName = DNS:$HOST,IP:10.10.10.20,IP:127.0.0.1 >> extfile.cnf
```

Set the Docker daemon key’s extended usage attributes to be used only for server authentication:

```bash
echo extendedKeyUsage = serverAuth >> extfile.cnf
```

Now, generate the signed certificate:

```bash
openssl x509 -req -days 365 -sha256 -in server.csr -CA ca.pem -CAkey ca-key.pem \
  -CAcreateserial -out server-cert.pem -extfile extfile.cnf
```
