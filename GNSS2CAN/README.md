---
cover: >-
  https://images.unsplash.com/photo-1488590528505-98d2b5aba04b?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwzfHx0ZWNofGVufDB8fHx8MTY3NTI3NDQwOA&ixlib=rb-4.0.3&q=80
coverY: 0
---

# XML Example:Transmitting GNSS Data Over CAN Bus.

In this example we will see how we can configure a ReXgen data logger to transmit the GNSS positioning data over the CAN Bus.

### Use Cases

* Easily inject real time location information into your CAN Bus.
* Feed real-time location information to your CAN Dashboard or Instrument Cluster.
* Use ReXgen as a GNSS module for your existing CAN data logger.

### Following GNSS Data will be transmitted via CAN 0 Bus:

* Latitude
* Longitude
* Altitude
* Speed Over Ground
* Ground Distance
* Course Over Ground
* Number Of Satellites
* Quality

## Documentation

Below image shows how each element are linked in the XML file.

![XML\_Link](https://itltdgithub.s3.ap-south-1.amazonaws.com/gnss2canonly.png)

They are connected with each other using the Unique IDs (UID).

### Default Settings

* CAN Baud Rate : 500 Kbps
* GNSS Sampling Rate : 100ms
* CAN ID For various signals:
* 0x12B – Altitude, GPS Speed
* 0x12C – Longitude, Latitude
* 0x12D – Ground Distance
* 0x12E – Number Of Satellites, Course
* 0x12F - Quality Example DBC provided with XML.

#### These parameters can be modified by editing the XML as required.

**Modifying CAN Bus Channel:**

Edit the value of PhysicalNumber element in the XML file under the CAN interface block. 0 for CAN 0, 1 for CAN 1, 2 for CAN 2 and 3 for CAN 3

<pre class="language-xml"><code class="lang-xml">&#x3C;CANINTERFACE UID="1">
        &#x3C;Type>CAN&#x3C;/Type>
        <a data-footnote-ref href="#user-content-fn-1">&#x3C;PhysicalNumber>0&#x3C;/PhysicalNumber></a>
        &#x3C;CANBusSpeed>500000&#x3C;/CANBusSpeed>
        &#x3C;CANFDBusSpeed>8000000&#x3C;/CANFDBusSpeed>
        &#x3C;CANFDNonISO>false&#x3C;/CANFDNonISO>
</code></pre>

**Modifying CAN Baud Rate:**

Edit the value of CANBusSpeed element in the XML file under the CAN interface block. Value has to be specified in bps

<pre class="language-xml"><code class="lang-xml">&#x3C;CANINTERFACE UID="1">
        &#x3C;Type>CAN&#x3C;/Type>
        &#x3C;PhysicalNumber>0&#x3C;/PhysicalNumber>
        <a data-footnote-ref href="#user-content-fn-2">&#x3C;CANBusSpeed>500000&#x3C;/CANBusSpeed></a>
        &#x3C;CANFDBusSpeed>8000000&#x3C;/CANFDBusSpeed>
        &#x3C;CANFDNonISO>false&#x3C;/CANFDNonISO>
</code></pre>

**Modifying GNSS Sampling Rate:**

Edit the value of Sampling  Rate element under the GNSSINTERFACE Block Value has to be specified in milliseconds

<pre class="language-xml"><code class="lang-xml">&#x3C;GNSSINTERFACE UID="2">
        &#x3C;PhysicalNumber>0&#x3C;/PhysicalNumber>
        <a data-footnote-ref href="#user-content-fn-3">&#x3C;SamplingRate>100&#x3C;/SamplingRate></a>
 &#x3C;/GNSSINTERFACE>

</code></pre>

**Modifying the CAN Identifier for the messages:**

Edit the values of MessageIdentStart and MessageIdentEnd Elements under the CANMESSAGE block for the message you wish to edit. Please not that the example DBC will be invalid after this change.

Value has to be entered in Decimal

<pre class="language-xml"><code class="lang-xml">&#x3C;CANMESSAGE_LIST>
      &#x3C;CANMESSAGE UID="3">
        <a data-footnote-ref href="#user-content-fn-4">&#x3C;MessageIdentStart>299&#x3C;/MessageIdentStart></a>
        <a data-footnote-ref href="#user-content-fn-5">&#x3C;MessageIdentEnd>299&#x3C;/MessageIdentEnd></a>
        &#x3C;Direction>OutputPeriodic&#x3C;/Direction>
        &#x3C;DLC>8&#x3C;/DLC>
        &#x3C;IsExtended>false&#x3C;/IsExtended>
</code></pre>

Modifying the CAN Message transmission period:

Edit the values of Period Elements under the CANMESSAGE block for the message you wish to edit.

Value has to be entered in milliseconds

<pre class="language-xml"><code class="lang-xml">&#x3C;CANMESSAGE_LIST>
      &#x3C;CANMESSAGE UID="3">
        &#x3C;MessageIdentStart>299&#x3C;/MessageIdentStart>
        &#x3C;MessageIdentEnd>299&#x3C;/MessageIdentEnd>
        &#x3C;Direction>OutputPeriodic&#x3C;/Direction>
        &#x3C;DLC>8&#x3C;/DLC>
        &#x3C;IsExtended>false&#x3C;/IsExtended>
        &#x3C;InterfaceUID>4&#x3C;/InterfaceUID>
        <a data-footnote-ref href="#user-content-fn-6">&#x3C;Period>100&#x3C;/Period></a>
</code></pre>

#### User can load the XML file into the ReXgen logger using ReXdesk application/ReXdesk Convert application or the Rxlibrary DLL

Process to send XML to logger using ReXdesk. Click on Config Menu > Run > Run Config Using External File > Browse the XML file and click Open

[^1]: Edit the value of PhysicalNumber element in the XML file under the CAN interface block. 0 for CAN 0, 1 for CAN 1, 2 for CAN 2 and 3 for CAN 3

[^2]: Edit the value of CANBusSpeed element in the XML file under the CAN interface block. Value has to be specified in bps

[^3]: Edit the value of Sampling Rate element under the GNSSINTERFACE Block Value has to be specified in milliseconds

[^4]: Edit the values of MessageIdentStart Element under the CANMESSAGE block for the message you wish to edit. Please not that the example DBC will be invalid after this change.

    Value has to be entered in Decimal

[^5]: Edit the values of MessageIdentEnd Element under the CANMESSAGE block for the message you wish to edit. Please not that the example DBC will be invalid after this change.

    Value has to be entered in Decimal

[^6]: Edit the values of Period Elements under the CANMESSAGE block for the message you wish to edit.

    Value has to be entered in milliseconds
