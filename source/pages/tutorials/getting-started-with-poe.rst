Getting started with PoE
########################

We currently have two Power-over-Ethernet (PoE) devices:
 - `OAK-D-POE <https://docs.luxonis.com/projects/hardware/en/latest/pages/SJ2088POE.html>`__ and
 - `OAK-1-POE <https://docs.luxonis.com/projects/hardware/en/latest/pages/SJ2096POE.html>`__

PoE allows a single Cat5e (or higher) Ethernet cable to be used to both power a device and give it connectivity
at 1,000 Mbps (1 Gbps) full-duplex at up to 100 meters (328 feet).

.. image:: https://user-images.githubusercontent.com/18037362/125928421-daed2432-73fb-4c5b-843e-037c7383a871.gif

*After connecting the PoE device, the Ethernet connectivity LED (shown above) should turn on and start occasionally flashing.*

Step by step tutorial
*********************

#. You will need a PoE switch or Injector **to power the PoE device**. `Click here for the full tutorial <https://docs.luxonis.com/projects/hardware/en/latest/pages/powering_poe_devices.html>`__. After powering the device, LED should start blinking, as on the GIF above.
#. Connect your computer to the same `LAN <https://en.wikipedia.org/wiki/Local_area_network>`__ as the PoE device
#. Make sure you have **depthai version 2.7.0.0** or newer. You can update your depthai python package with :code:`python3 -m pip install depthai>=2.7.0.0`
#. Now you can run any `code sample <https://docs.luxonis.com/projects/api/en/latest/tutorials/code_samples/>`__ / `depthai experiment <https://github.com/luxonis/depthai-experiments>`__ / `depthai_demo <https://github.com/luxonis/depthai>`__ as you would when connecting a DepthAI device with a USB-C cable!

.. image:: /_static/images/tutorials/poe/poe-working.jpeg

*After these steps, the depthai_demo is working on the OAK-D-POE!*

How it works
************

When your program tried to create the device (:code:`with dai.Device(pipeline) as device:`),
the library will search for available devices that are connected either by USB port or on the LAN.
It searches for PoE devices on the same network (eg. LAN) and communicates over TCP protocol.
That way PoE devices work in same manner as USB devices. As with theUSB-C connection, you can specify
the Mx ID to specify to which DepthAI PoE device you would want to connect to
(`more info here <https://docs.luxonis.com/projects/api/en/latest/tutorials/multiple/>`__).


PoE Troubleshooting
*******************

- **DHCP and Static IP**
    By default, PoE devices will try to pull an IP address from DHCP. If a DHCP server isn't available on the network,
    devices will fall back to static IP :code:`169.254.1.222`.  In this static fall-back case, your computer will need to be in the same range. This can
    be achieved by setting a static IP on your computer (e.g. with static IP: :code:`169.254.1.10` and netmask: :code:`255.255.0.0`).

- **Ports and Firewall**
    UDP Device discovery is handled on port :code:`11491`, and TCP XLink connection is handled on port :code:`11490`.
    
    On Ubuntu by default the firewall is disabled, so you shouldn't have any issues. You can check this though by executing the following command:

    .. code-block:: bash

      > sudo ufw status
      Status: inactive

    If you have your firewall enabled, you might need to allow these two ports:

    .. code-block:: bash

      sudo ufw allow 11490/tcp
      sudo ufw allow 11491/udp

- **VPN connection**
    VPN connectivity could also disrupt the connection with the PoE device (as your computer may be searching only the remote network for the device, so would be unable to discover it on the local network), so we suggest turning the VPN off when using the PoE devices or otherwise ensuring that your local routing is setup such that local devices are usable/discoveragle while VPN connectivity is active.


.. include::  /pages/includes/footer-short.rst
