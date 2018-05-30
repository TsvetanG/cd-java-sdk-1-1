# cd-java-sdk-1-1
Java SDK based client for Fabric 1.1


-- Private collection json file is located in store folder (collections-cli.json). It defines two private collections. This file should be used to instantiate or/and upgrade the chancode. The file should be copied to the CLI host machine so it may be accessed by the CLI docker container.

-- To install, invoke and query use the Java classes related to the node js chaincode (they are named accordingly)

-- The following commands in CLI will instantaite / upgrade the chaincode. Note the JAVA SDK at the moment doesn't have APIs to add a private data collection definition hence the process is done from CLI.

Instantiate command from Fabric CLI:
export ORDERER_CA_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/funds.com/orderers/fundorderer.funds.com/msp/tlscacerts/tlsca.funds.com-cert.pem

peer chaincode instantiate -o fundorderer.funds.com:7050 -n nodecccc --collections-config /opt/gopath/src/github.com/hyperledger/fabric/peer/scripts/collections-cli.json -v 1 -c '{"Args":["init","alice","100","bob","50"]}' -P "OR ('maple.member', 'fundinc.member')" --cafile $ORDERER_CA_FILE --channelID transfer

Upgrade command from Fabric CLI:
export ORDERER_CA_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/funds.com/orderers/fundorderer.funds.com/msp/tlscacerts/tlsca.funds.com-cert.pem

peer chaincode upgrade -o fundorderer.funds.com:7050 -n nodecccc --collections-config /opt/gopath/src/github.com/hyperledger/fabric/peer/scripts/collections-cli.json -v 17 -c '{"Args":["init","alice","100","bob","50"]}' -P "OR ('maple.member', 'fundinc.member')" --cafile $ORDERER_CA_FILE --channelID transfer
