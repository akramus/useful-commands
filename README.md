# Useful commands
## Git
Delete branches that no more exist on remote 
> git fetch -p && for branch in $(git branch -vv | grep ': gone]' | awk '{print $1}'); do git branch -D $branch; done


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
> openssl pkcs12 -export -inkey fichier_cle -in fichier_certificat -chain -CAfile fichier_chaine_de_certification -name alias_certificat -out fichier_pkcs12

with :

    fichier_chaine_de_certification = fichier contenant tous les certificats d'AC de la chaîne de certification (base64) concaténés
    alias_certificat = nom arbitraire pour identifier le certificat dans le keystore (ce nom sera utile pour importer le keystore PKCS#12 produit dans un keystore JKS avec la commande keytool)

Lister un keystore PKCS#12
openssl pkcs12 -in fichier_pkcs12

Options utiles :

    -nodes = ne pas chiffrer la clé privée extraite
    -nokeys = ne pas extraire la clé privée
    -nocerts = ne pas extraire les certificats
    -clcerts = n'extraire que le certificat final
    -cacerts = n'extraire que les certificats d'AC de la chaine de certification    
