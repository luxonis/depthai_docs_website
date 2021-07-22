ESP32 tutorial
==============

.. note::
  This tutorial is intended for `OAK-D with WiFi <https://docs.luxonis.com/projects/hardware/en/latest/pages/DM1098OBC.html>`__
  and `LUX-ESP32 <https://docs.luxonis.com/projects/hardware/en/latest/pages/DM1092.html>`__, which both have an ESP32 on
  the board.

.. note::
  Having ESP32 on the device doesn't mean users will be able to develop the device without the USB-C connection.

**In this tutorial we will have a look at:**

- Overview of the ESP32 - DepthAI connection
- Limitations
- Common use cases for the ESP32
- How to get started with the development

Code examples
#############

Code examples can be found in our `esp32-spi-message-demo <https://github.com/luxonis/esp32-spi-message-demo>`__
github repository.

Overview
########

.. code-block::

                  DepthAI device                        ┌─────┐
  ┌───────────────────────────────────────────────┐     │  ◎  │
  │                                               │     │     │
  │                ┌───────────────────ESP32───┐  │  BT |     |
  │                │                           │--│◄───►|     |
  │                │   (Your ESP32 firmware)   │  │     └─────┘
  │                │                           │  │         ┌──────────┐
  │                │---------------------------│  │         │          │
  │                │     depthai-spi-api       │--│◄───────►├──────────┤
  │                └───────▲───────────────────┘  │  WiFi   │  Server  │
  │                        │                      │         ├──────────┤
  │                        │SPI                   │         │          │
  │      Right             │                      │         └──────────┘
  │       ┌───┐   ┌───┬────▼───┬─MyriadX(VPU)──┐  │
  │       │ ◯ │--►|   │        │               │  │            Host
  │ ┌───┐ └───┘   │   │ SpiOut │     ┌─────────┤  │        ┌───────────┐
  │ │ ◯ │--------►|   └────────┘     │         │  │        │           │
  │ └───┘ ┌───┐   │                  │ XLinkIn │  │  XLink │           │
  │Color  │ ◯ |--►| (Your pipeline)  │ XLinkOut│--│◄──────►│           │
  │       └───┘   │                  │         │  │        └────┬─┬────┘
  │        Left   └──────────────────┴─────────┘  │             │ │
  │                                               │           ──┴─┴──
  └───────────────────────────────────────────────┘

Overview explained:

- `MyriadX <https://www.intel.com/content/www/us/en/products/details/processors/movidius-vpu/movidius-myriad-x.html>`__ is the VPU on the DepthAI, where you can run your pipeline
- MyriadX is connected to the host (eg. PC)
- MyriadX can send `Messages <https://docs.luxonis.com/projects/api/en/latest/components/messages/>`__ to the ESP32 via SPI (using `SPIOut <https://docs.luxonis.com/projects/api/en/latest/components/nodes/spi_out/>`__ node)
- ESP32 can receive these messages using the `depthai-spi-api <https://github.com/luxonis/depthai-spi-api>`__ library (which is an `ESP-IDF <https://github.com/espressif/esp-idf>`__ component).
- On ESP32 you can run post-processing of the messages and optionally send the results to a server (if connected to a WiFi network) or to a Bluetooth device (eg. a smartphone)

Limitations
###########

Currently, the bottleneck for use cases is the SPI throughput, which is about **200kbps**.
This means you can't stream frames over SPI in real-time. This is the current limitation by the SPI driver, but we are planning
to look into it and increase the throughput of the SPI to **~8mbps** (no ETA yet).

As of now we only support `ESP-IDF <https://www.espressif.com/en/products/sdks/esp-idf>`__ as the development framework. In the future,
we might support `Arduino <https://github.com/espressif/arduino-esp32>`__.

Common use cases for the ESP32
##############################

**TL;DR:**

- Sending metadata results (spatial coordinates, NN results, tracklets etc.)
- OTA updates
- Capturing and sending (part of) an image
- System information logging
- Sending data to the cloud (eg. AWS/Azure/GCP or any other IOT platform)
- Sending data to a Bluetooth device (eg. smartphone)

**Explained in more detail:**

- You could run spatial object detections and/or object tracking pipeline on the VPU and send tracklets with spatial data over the SPI to the ESP32. On ESP32 you could run some simple filtering and/or NN result decoding and then send final results to the cloud
- ESP32 can also flash DepthAI bootloader and/or pipeline, which means OTA (over-the-air) updates are supported.
- We have an example for both sending a `whole image <https://github.com/luxonis/esp32-spi-message-demo/tree/main/jpeg_demo>`__ and `part of an image <https://github.com/luxonis/esp32-spi-message-demo/tree/main/image_part>`__ through the SPI from the VPU to the ESP32
- Pipeline on the VPU could be configured to send system information (using `SystemLogger <https://docs.luxonis.com/projects/api/en/latest/components/nodes/system_logger/>`__ node) to the ESP32 which would forward them to a logging platform
- ESP32 also has Bluetooth capabilities, so you could forward the data from the ESP32 to a smartphone

How to get started with the development
#######################################

#. Install the ESP-IDF, `instructions here <https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html#installation-step-by-step>`__.
#. After setting up the `environmental variables <https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html#step-4-set-up-the-environment-variables>`__, you can build any demo from the `esp32-spi-message-demo <https://github.com/luxonis/esp32-spi-message-demo>`__ repository with :code:`idf.py build`.
#. After building, you can flash your ESP32 using :code:`idf.py -p PORT flash monitor` (replace :code:`PORT` with the ESP32 port, eg. :code:`/dev/ttyUSB0`). You might need to change the permission of the port with :code:`sudo chmod 777 PORT` so idf.py can access it.
#. After flashing the ESP32, you can start the pipeline. If you have used a demo ESP32 code, you should run the corresponding python script from `gen2-spi demos <https://github.com/luxonis/depthai-experiments/tree/master/gen2-spi>`__.

.. include::  /pages/includes/footer-short.rst
