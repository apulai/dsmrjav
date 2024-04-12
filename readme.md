**Goal**

The goal of this repo is to allow easy testing of various fixes, for
dsmr_parser/clients/protocol.py

When this file is used by an integration in HomeAssistant and
the user is trying to parse an EON Hungary telegram the code raises 
an exception and dies. In fact EON Hungary is sending non-ascii 
charaters in it's telegram (0xff chars).

There are 4 different test fixes in this test repo:

- use a try and a except block and in the except part
encode and decode telegram with latin1 instead of ascii
- use a try and pass block
- use decode("ascii","ignore)
- use decode("ascii","backslashreplace")

**How to use**

Start HomeAsssitant's web userinterface.
Open AdvTerminal and SSH console on the web interface.

Then jump into the homeassistant container and
clone this repo to /tmp. They copy on of the fixes to
/usr/local/lib/python3.12/site-packages/dsmr_parser/clients/.

<pre>
docker exec -it homeassistant /bin/bash
cd /tmp
git clone https://github.com/apulai/dsmrjav
cd  /usr/local/lib/python3.12/site-packages/dsmr_parser/clients/
cp protocol.py protocol.py.orig

cp /tmp/dsmrjav/clients/protocol.jav_pass.py protocol.py
or
cp /tmp/dsmrjav/clients/protocol.jav_w2latin1.py protocol.py
or
cp /tmp/dsmrjav/clients/protocol.jav_wbsr.py protocol.py
or
cp /tmp/dsmrjav/clients/protocol.jav_ignore.py protocol.py`
</pre>

Happy testing