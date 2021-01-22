# Useful commands
## Git
Delete branches that no more exist on remote 
> git fetch -p && for branch in $(git branch -vv | grep ': gone]' | awk '{print $1}'); do git branch -D $branch; done

force pull to overwrite local files
> git fetch --all  && git reset --hard origin/master && git pull origin master

## netstat

To list the TCP ports that are being listened on
> sudo netstat -plnt

To list all listennig ports (tcp and upd)
> sudo netstat -ltup

## openssl 

Base64 encode a file  

> openssl enc -e -a -in fichier_to_encode

Useful options :
    -A = delete  all line breaks every 64 caracters



Decode  base64 fichier file
> openssl enc -d -a -in file_to_encode

Useful options :
    -A = decode a base64 string without lines break every 64 caracters

file sha-1 encode base64
> openssl sha1 -binary file | base64 

Create RSA key
> openssl genrsa key_length >key_file

with:

    key_length = key length de la bits (ex. : 2048)

Display a private RSA key
> openssl rsa -text -noout -in key_file

Unprotect a private RSA key

> openssl rsa -in key_file

Useful options :

    -passin "pass:password" = put the key password in command line

Extract public key from a private RSA key

> openssl rsa -pubout -in key_file > public_key

Display ECC curves supported by OpenSSL

> openssl ecparam -list_curves

Create a ECC private key

> openssl ecparam -name curve_name -genkey >key_file

with :

    curve_name = curve name to user (ex. : prime256v1)

Display a private ECC key

> openssl ec -text -noout -in key_file

Unprotect a private ECC key

> openssl ec -in key_file

Useful options :

    -passin "pass:password" = put the key password in command line

Extract a public key from a private ECC key

> openssl ec -pubout -in key_file >public_key_file

Dispaly a CSR
> openssl req -text -noout -in csr_file

Display a certificate

> openssl x509 -text -noout -in certificate_file

Extract a public from a certificate file
> openssl x509 -pubkey -noout -in certificate_file >certificate_public_file

Check a certificat with CA file
> openssl verify -CAfile CA_File certificate_file_to_check

with :

    CA_File = file containing all tous AC certificates used to check a format (base64) concatened

Create a keystore PKCS#12
> openssl pkcs12 -export -inkey key_file -in certificate_file -chain -CAfile CA_file -name alias_certificate -out file_pkcs12

with :

    CA_file = file containing all certificates AC (base64) concatened
    alias_certificate = name to pour indentify  certificate in keystore (

Display a keystore PKCS#12

> openssl pkcs12 -in fichier_pkcs12

Useful options :

    -nodes = Not encrypt private key 
    -nokeys = Not extract private key 
    -nocerts = Not extract certificated
    -clcerts = Extract only final certificate
    -cacerts = Extract only AC certificates  
    
    
Display exposed certificat by server  

> openssl s_client -connect hostname:port -showcerts
 
The result is orgnized in multiple sections 
- SSL/TLS connection status summary.
- Server certificat and it AC displayed in  PEM/base64 foramt (section Certificate chain).
- Certificae name and AC that genertaes the certificate (section Server certificate).
- Trust AC list names  to de authenticate client certificates  (section Acceptable client certificate CA names).
- Other SSl/TLS parameters(sections Client Certificate Types, Requested Signature Algorithms, Shared Requested Signature Algorithms, Peer signing digest, Server Temp Key).
- SSL/TLS detailed connection status.

## Keytool

Display a certificate

> keytool -printcert -file fichier_certificat

Display keystore content
> keytool -list -keystore fichier_keystore

Options  :
    - storetype to define keystore type: JKS (defult value), PKCS12, JCEKS
    - v detail in text format
    - rfc PEM format

Exporter a certificat from a JKS keystore

> keytool -exportcert -keystore fichier_keystore_jks -alias alias_certificat -file fichier_certificat

Exporter a PKCS#12 keystore from  JKS keystore

> keytool -importkeystore -srckeystore fichier_keystore_jks -destkeystore fichier_keystore_pkcs12 -srcstoretype JKS -deststoretype PKCS12 -srcalias alias_cle_privee -destalias alias_cle_privee

Import a certificate JKS keystore 

> keytool -importcert -noprompt -trustcacerts -keystore fichier_keystore_jks -alias alias_certificat -file fichier_certificat

Imoort a keystore PKCS#12 keystore  into JKS keystore

> keytool -importkeystore -srckeystore fichier_keystore_pkcs12 -destkeystore fichier_keystore_jks -srcstoretype PKCS12 -deststoretype JKS -srcalias alias_cle_privee -destalias alias_cle_privee

Create a trustore
> keytool -import -file certificate -alias firstCA -keystore myTrustStore

## tools
checksum  and encode in base 64
> md5sum -t Makefile |awk '{print $1}'|base64.exe 
