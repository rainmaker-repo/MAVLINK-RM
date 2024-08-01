## Rainmaker MAVLink Fork

# Installation

To install the Rainmaker MAVLink fork, follow these steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/rainmaker-repo/MAVLINK-RM.git --recursive
   cd MAVLINK-RM
   ```

2. Install the required dependencies:
   ```bash
   sudo apt install python3-pip
   python3 -m pip install -r pymavlink/requirements.txt
   ```

3. Generate the MAVLink headers:
   ```bash
   python3 -m pymavlink.tools.mavgen --lang=C --wire-protocol=2.0 --output=generated/include/mavlink/v2.0 message_definitions/v1.0/common.xml
   ```

This will set up the Rainmaker MAVLink fork on your system with the necessary dependencies and generate the required headers.

# Adding New Messages
To add new custom MAVLink messages for the Rainmaker fork, follow these steps:

1. Add new messages to the existing rainmaker.xml:
   - Navigate to the `message_definitions/v1.0/` directory.
   - Open the existing `rainmaker.xml` file.
   - Add your new message definitions using the MAVLink XML format.
   - Example of adding a new message:
     ```xml
     <message id="502" name="RAINMAKER_CUSTOM_MSG">
       <description>A custom message for Rainmaker</description>
       <field type="uint64_t" name="timestamp" units="us">Timestamp (microseconds since system boot)</field>
       <field type="float" name="data_value">Custom data value</field>
     </message>
     ```

2. The rainmaker.xml is already included in the common dialect:
   - The `common.xml` file in the `message_definitions/v1.0/` directory already includes rainmaker.xml:
     ```xml
     <include>rainmaker.xml</include>
     ```
   This ensures that your custom messages are included in the main MAVLink dialect.

3. Generate the headers:
   - When you build the common dialect, it will automatically include the rainmaker messages.
   - Run the MAVLink generator to create updated C headers including your new messages:
     ```
     python3 -m pymavlink.tools.mavgen --lang=C --wire-protocol=2.0 --output=generated/include/mavlink/v2.0 message_definitions/v1.0/common.xml
     ```
   This command will generate headers that include both the common messages and your custom Rainmaker messages.
