# beskrivelse
Util:

const PUB_PEM
const PRIV_PEM
const CMD_KEYGEN
const CMD_CONCEAL
const CMD_DECONCEAL
const SUCI_FILE_NAME
const KDF_APP_INFO
const ENTITY_NAME_HOME

func cmd_arg
func err_print
func gen_ECDH_key_pair
func serialize_pub_key
func store_public_key
func store_private_key
func load_public_key
func load_private_key
func key_derivation
func add_len_prefix
func add_padding

Home:
const PRIVPW
const cmd
# CMD deconceal


User:
# CMD conceal


Generelt:
Tenk input og output.
Input: melding med ECDH key pair, 

HOME dekrypterer SUCI med sin private nøkkel og får tilbake SUPI.
UE krypterer SUPI med nettets public key.
HOME dekrypterer med private key.

    Dette er hovedtrekkene:
    • «SUCI» lignende måte å utveksle personvern-sensitive identifikator
    • Bruk av ECDH og SECP256R1 kurven
    • Bruk av ConcatKDFHhash    
    • Bruk av AEAD (AES-GCM)

    SUCI_data.bin:
    IV: 16 bytes; # pseudo-random number; Integrity protected.
    home_ID: 64 bytes; # encoded Home identifier. Integrity protected.
    user_pub: 180 bytes; # encoded User public key. Integrity protected.
    ct: 80 bytes; # ciphertext og user_ID (includes the tag)

    Fra test 1:
        IV (hex): 90f3c8d9853901422c2a975d4e24335a
        home_ID (raw): 000d7369646640686f6d652e6f726700000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
        home_ID (utf-8): 
        user_pub length: 180 bytes
        ct length:       80 bytes

    • The IV is not encoded. Fixed length.
    • The home_ID (and user_ID) are fields of 64 bytes and encoded as
    follows:
    len><utf-8-name><padding>


To-do:

    Input: Er laget i test dataene. 
    I - 

    Output: SUCI-data (?)
    Skrive ferdig output meldingen - spesifisert DECONCEAL (print funksjoner som er linket riktig til forskjellige funksjoner)

Om hele metoden:
Asymmetrisk kryptering (public/private key).
Konfidensialitet av identitet (SUPI) over luftgrensen.

