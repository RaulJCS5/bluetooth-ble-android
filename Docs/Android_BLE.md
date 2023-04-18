# Android and Bluetooth Low Energy

## Basics

Android provides built-in APIs that apps can use to discover devices.

Common use cases include the following:
- Transferring small amounts of data between nearby devices.
- Interacting with proximity sensors to give users a customized experience based on their current location.

``BLE`` is designed for significantly lower power consumption.

For ``BLE``-enabled devices to transmit data between each other, they must first form a channel of communication. ``BLE`` APIs requires you to [declare several permissions](https://developer.android.com/guide/topics/connectivity/bluetooth/permissions) in your manifest file. Once your app has permission to use Bluetooth, your app needs to access the BluetoothAdapter and [determine if Bluetooth is available on the device](https://developer.android.com/guide/topics/connectivity/bluetooth/setup). If Bluetooth is available, the device will [scan for nearby BLE devices](https://developer.android.com/guide/topics/connectivity/bluetooth/find-ble-devices). Once a device is found, the capabilities of the ``BLE`` device are discovered by [connecting to the GATT server on the BLE device](https://developer.android.com/guide/topics/connectivity/bluetooth/connect-gatt-server). Once a connection is made, [data can be transferred with the connected device](https://developer.android.com/guide/topics/connectivity/bluetooth/transfer-ble-data) based on the available services and characteristics.

## Key terms and concepts

- Generic Attribute Profile (``GATT``)
    - is a general specification for sending and receiving short pieces of data known as "attributes" over a ``BLE`` link.
    [Android BluetoothLeGatt sample](https://github.com/android/connectivity-samples/tree/master/BluetoothLeGatt) 
- Profiles
    - A profile is a specification for how a device works in a particular application.
- Attribute Protocol (``ATT``)
    - ``GATT`` is built on top of the Attribute Protocol (``ATT``). It uses as few bytes as possible. Each attribute is uniquely identified by a Universally Unique Identifier (``UUID``), which is a standardized 128-bit format for a string ``ID`` used to uniquely identify information.
- Characteristic
    - A characteristic contains a single value and 0-n descriptors
- Descriptor
    - Descriptors are defined attributes that describe a characteristic value.
- Service
    - A service is a collection of characteristics. For example, you could have a service called "Heart Rate Monitor" that includes characteristics such as "heart rate measurement."

## Roles and responsibilities

### **Central versus peripheral**

The device in the central role scans, looking for advertisement, and the device in the peripheral role makes the advertisement.

### **GATT server versus GATT client**

This determines how two devices talk to each other once they've established the connection. Two things that only support peripheral couldn't talk to each other, nor could two things that only support central.

**For example:**

Once the phone and the activity tracker have established a connection, they start transferring GATT metadata to one another. Depending on the kind of data they transfer, one or the other might act as the server. For example, if the activity tracker wants to report sensor data to the phone, it might make sense for the activity tracker to act as the server. If the activity tracker wants to receive updates from the phone, then it might make sense for the phone to act as the server.

## Bluetooth permissions

### Target Android 12 or higher