Sl No
Attribute
Required?
Value
1
.
ver
Mandatory
eSign  version  (mandatory).  ESP  may  host  multiple versions  for  supporting  gradual  migration.  As  of  this specification, 
APIVersion is “2.0”.
2
.
sc
mandatory
sc 
–
(mandatory) 
ASP  should  have  taken  a  clear 
consent from ‘eSign  user’ to carry on eSign from their    front    ending    application.    This    attribute represents signatory’s explicit consent is obtained by ASP for using the signatory’s identity and address  data 
received 
from 
e
-
KYC
provider  to
,  generate  and 
submit
the
electronic  DS
C  application  form  to  CA, 
creation of key pairs by ESP
for signatory, submission 
of   certificate   to   CA   for   certification,
one   time 
creation  of  signature
on  the  hash
along  with  this 
request,
deletion of
key pairs from the
after
applying
signature. 
Only valid
value is “Y”.
Check box[Y/N*]
*No by default
3
.
t
s
Mandatory
Request timestamp in ISO format
. 
The  value  should  be  in  Indian  Standard  Time  (IST), 
and  should  be  within  the  range  of  maximum  30 
8
minutes   deviation   to   support   out   of   sync   server 
clocks.
4
.
t
xn
M
andatory
Transaction  ID  of  the  ASP  calling  the  API,  this  is 
logged and returned in the output for correlation
5
.
e
-
KYC
Mode
Mandatory
This  represents  the  mode  of 
e
-
KYC
being  used.
The 
value can be any one out of below:
1
.
UIDAI
= U
6
.
e
-
KYC
IdType
Mandatory
Thi
s
represent
s
the 
type 
of 
e
-
KYC
ID being used
.
The 
value can be any one out of below:
1
.
Aadhaar
= A
7
.
ekycId
Mandatory
ekyc 
identity  Number  of  the 
eSign  user
.
The  value 
can be any one out of below:
1
.
12 digit Aadhaar Number
8
.
asp
I
d
Mandatory
Organization 
I
D issued by ESP to the ASP
9
.
AuthMode
Mandatory
Authentication     Mode 
being     used     for 
e
-
KYC
Authentication, either to be performed by ESP, or as 
already made by the ASP
.
Allowed values are:

OTP 
= 1

Fingerprint 
= 2
(only for eKycMode = U)

IRIS = 3
(only for e
KycMode = U)

---


Class of eSign Certificate will be “OTP Class” for OTP 
based  authentication.  For  Fingerprint  and  IRIS,  the 
class will be “Biometric Class”. These will be as per 
definitions of “Class of Certificate” in India PKI
-
CP.
10
.
responseSigType
Mandator
y
This  value  represents  the  response  signature  type, 
where ASP can request for specific type of signature, 
like Raw or PKCS7.
Allowed Values are:
1
.
raw
rsa
2
.
pkcs7
Examples:
responseSigType="raw
rsa
"
responseSigType="pkcs7"
11
.
preVerified
Mandatory
Represents 
w
hether
ASP  has  already  made  a 
e
-
KYC
transaction  towards  the 
eSign  user
.  (Not  older  than 
15 minutes)
Allowed values are y 
and n
representing yes
& 
no.
If   Yes,   the   sub
-
element 
AspKycData
is   required. 
ESP
/CA
will   verify   the   integrity   by   validating 
e
-
KYC
Prov
ider 
signature  on 
AspKycData
,  and  then  use 
respective 
KYC
information    to    generate    Digital 
Signature 
Certificate.
9
Else, 
ESP  should  authenticate  the  user  and  obtain 
KYC information from 
available 
eKycMode.
12
.
organizationFlag
Optional
Represents  that  the  req
uest  is  for  an  Organization 
Certificate.
Allowed values are y and n, representing yes or no.
If  yes,  the  sub
-
element  OrgDetails  is  required.  ESP 
shall  operate  a  verified  information  of  Organization 
and    have    the    authorized    signatory    certificate 
mapped in 
the system. The OrgDetails XML signature 
should be  verified  against  the  certificate available  at 
ESP end, for the data integrity and signature.
13
.
responseUrl
Optional
This is mandatory, if preverified is set to ‘no’.
This should contain a valid HTTPS URL o
f the ASP, to 
which ESP has to 
redirect back to ASP
with response 
XML
.
Element Name: Docs

Description: Contains minimum 1, maximum of 10 sub
-
elements with Document Hash

Requirement of tag: Mandatory

Value: Sub
-
elements

Attributes: Not applicable
Element
Name: 
I
nput
Hash

Description: Contains the value of Document Hash, which has to be signed.

Requirement of tag: Mandatory

Value: 
SHA256 
hash value of the document
in Hex format

Attributes: 
Table below
Sl No
Attribute
Required?
Value
1
.
id
Mandatory
Contains
running    serial    number    for    document 
hashes.   This   should   start   at   1,   and   should   be 
sequential, maximum up
-
to 10.
This   will   be   the   key   to   correlate   the   response 
signature of each document.
2
.
h
ashAlgorithm
Mandatory
Should be fixed to “SHA256”
3
.
docInfo
Mand
atory
Description   for   the   respective   document   being 
signed, not more than 50 char/

---

with <3

(C) itsN1X
