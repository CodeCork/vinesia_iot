# Project Description - IoT Gateway

The Vinesia IoT Gateway is a system designed to connect the Internet of Things (IoT) devices with the canisters on the Internet Computer. It enables both inbound and outbound traffic. The project is composed of three components: the gateway, candid specification, and example storage canister. The gateway facilitates the transfer of data between IC and MQTT and requires configuration to connect to a specific MQTT broker. The candid specification provides a standardized method for IC canisters to interact with the gateway. When set up correctly, the canister can both receive and send messages to the MQTT protocol broker on designated topics. The example storage canister offers a straightforward demonstration of how to receive, send, and store data using the gateway.

# Architecture

## Topic name structure

Topic name that can be handled by the gateway:
`canisterId`:`topic`

---

## Target Canister Specifics

Three endpoints
- update: onMessage(topic: string, data: string) - receives MQTT messages
- query: getMessages(index: int): MessageResult - get latest messages, max 100 messages

- query: getSettings(): Settings - returns canisters settings related to MQTT channels processing

---

## Canister Settings
- interval - how often canister should be queried for messages: 0 do not query, otherwise query interval in seconds
- owner - the principal that can use `onMessage`, if none then anyone can

---

# Requirements
- DFX - 0.14.2
- NODE - v16 or higher
- YARN
- RUST - v1.69 or higher with wasm32-unknown-unknown target
- DOCKER - for launching mosquitto mqtt broker

---

# How to Run

1. Install all packages using `yarn`
2. Build canister `yarn buid`
3. Generate local gateway key for testing `node generate_key.js`
4. Run mosquitto mqtt broker
```
cd test
docker-compose up -d
```
5. Run mock sensor `node data_mock.js`
6. Deploy storage canister `yarn devenv`
7. Run gateway `node gateway.js`