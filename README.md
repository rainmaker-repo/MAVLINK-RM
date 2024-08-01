## Rainmaker MAVLink Fork

# Adding New Messages
To add new custom MAVLink messages for the Rainmaker fork, follow these steps:

1. Create a new XML file:
   - Navigate to the `message_definitions/v1.0/` directory.
   - Create a new XML file (e.g., `rainmaker.xml`) for your custom messages.

2. Define your messages:
   - Open the new XML file and add your message definitions using the MAVLink XML format.
   - Example:
     ```xml
     <?xml version="1.0"?>
     <mavlink>
       <include>common.xml</include>
       <messages>
         <message id="50000" name="RAINMAKER_CUSTOM_MSG">
           <description>A custom message for Rainmaker</description>
           <field type="uint32_t" name="timestamp" units="ms">Timestamp of the message</field>
           <field type="float" name="data_value">Custom data value</field>
         </message>
       </messages>
     </mavlink>
     ```

3. Include your custom dialect:
   - Open the `development.xml` or `common.xml` file in the `message_definitions/v1.0/` directory.
   - Add an include statement for your new XML file just after the other include statements:
     ```xml
     <include>rainmaker.xml</include>
     ```
   This ensures that your custom messages are included in the main PX4 dialect. PX4 uses `common.xml` as the main dialect.

3. Generate the headers:
   - Run the MAVLink generator to create updated C headers including your new messages.
   - Use a command such as:
     ```
     python3 -m pymavlink.tools.mavgen --lang=C --wire-protocol=2.0 --output=generated/include/mavlink/v2.0 message_definitions/v1.0/rainmaker.xml
     ```
