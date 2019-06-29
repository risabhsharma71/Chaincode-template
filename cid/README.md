Client Identity Library
=======================
https://github.com/hyperledger/fabric/tree/release-1.1/core/chaincode/lib/cid
https://golang.org/pkg/crypto/x509/

Users in acme
=============
- mary
"app.accounting.role=tradeapprover:ecert","department=accounting:ecert"
- john
"app.accounting.role=accountant:ecert","department=accounting:ecert"
- anil
"department=logistics:ecert"

# Make sure the context is admin otherwise the instantiate will Fail
# with endrosement error
. set-env.sh acme
. set-ca-msp.sh admin

set-chain-env.sh -n cid -v 1.0  -p token/cid -c '{"Args":["init"]}'

chain.sh install
chain.sh instantiate

set-chain-env.sh  -q '{"Args": ["ReadAttributesOfCaller"]}'


Query
=====

set-chain-env.sh  -i '{"Args": ["AsssertOnCallersDepartment"]}'

. set-ca-msp.sh  mary
chain.sh invoke

. set-ca-msp.sh  john
chain.sh query

. set-ca-msp.sh  anil
chain.sh query

Invoke
======
. set-ca-msp.sh  mary
chain.sh invoke

. set-ca-msp.sh  john
chain.sh query

. set-ca-msp.sh  anil
chain.sh query


