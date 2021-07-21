First steps with DepthAI
========================

Hello DepthAI users!

In this guide, I assume you just got your DepthAI device (e.g. `OAK-1 <https://docs.luxonis.com/projects/hardware/en/latest/pages/BK1096.html>`__ or `OAK-D <https://docs.luxonis.com/projects/hardware/en/latest/pages/BW1098OAK.html>`__)
and you want to give it the first try to explore what is possible with it and what you can achieve when working with it.

- First, we will run a DepthAI demo script, that will allow you to preview DepthAI functionalities.
- Next, I will explain what the script does and describe basic terms used in the DepthAI world.
- Following up, I will show which models you can run on the DepthAI out-of-the-box and how to run a custom model.
- Last, you will receive useful links to expand your knowledge further, and check open-sourced use-case implementations, code examples and tutorials, that you can use as a starting point for your projects.

Let's start with the device setup below

Watch the video
###############

If you prefer, we've encapsulated this tutorial in a short YouTube video you can follow along while scrolling this page

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube.com/embed/LN1O9vhPJA0" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>

Connect the DepthAI device
##########################

After unboxing your DepthAI package, you will receive your device together with a USB-C cable (and a power supply if you ordered OAK-D)

Make sure that the device is connected to your host (which can be a PC or Raspberry Pi or another capable device) directly to a USB port,
or via a powered USB hub.

On Ubuntu, you can check if a new USB device was detected by running

.. code-block:: bash

  $ lsusb | grep MyriadX
  Bus 003 Device 002: ID 03e7:2485 Intel Movidius MyriadX

.. note::

  If you are running other OS than Ubuntu, or you think something has gone wrong, we have detailed OS-specific installation guides
  `here <https://docs.luxonis.com/projects/api/en/latest/install/#supported-platforms>`__, together with discord support
  channels where you can chat with us live if you have any issues or questions.

Download demo script
####################

Our goal is to make engineering efficiency higher with DepthAI. As a part of this effort, we created an all-in-one script that
allows you to check DepthAI features using command line arguments - no coding required!

To download the demo script, you can either use :code:`git` or directly download a zip file

From zip file
*************

First, download a repository package from `here <https://github.com/luxonis/depthai/archive/refs/heads/main.zip>`__
and then unpack the archive to a directory of preference. Next open a terminal session in this directory.

From git
********

First, open the terminal session and go to a directory of preference, where you'd like to download your demo script.
Then, run the following code to download the demo script

.. code-block:: bash

  $ git clone https://github.com/luxonis/depthai.git

After the repository is downloaded, make sure to enter the downloaded repository by running

.. code-block:: bash

  $ cd depthai

Create python virtualenv (optional)
###################################

To create and use the virtualenv, you can follow an `official python guide to virtualenvs <https://docs.python.org/3/tutorial/venv.html>`__ or
follow os-specific guides on the web, like `"How to Create Python 3 Virtual Environment on Ubuntu 20.04" <https://linoxide.com/how-to-create-python-virtual-environment-on-ubuntu-20-04/>`__

This will make sure that you are using a fresh environment and that Python 3 is the default interpreter - this can help to prevent potential issues.

I usually create and use virtualenvs by running

.. code-block:: bash

  $ python3 -m venv myvenv
  $ source myvenv/bin/activate
  $ pip install -U pip

And this may require installing these packages prior

.. code-block:: bash

  $ apt-get install python3-pip python3-venv

Install requirements
####################

Once the demo source code is downloaded, and you have your terminal session set up, the next thing that has to be done
is to install all additional packages that this script requires (together with the :code:`depthai` Python API itself).

To install these packages, run the :code:`install_requirements.py` script

.. code-block:: bash

  $ python3 install_requirements.py

.. warning::

  If you are using a Linux system, in most cases you have to add a new udev rule for our script to be able to access
  the device correctly. You can add and apply new rules by running

  .. code-block:: bash

    $ echo 'SUBSYSTEM=="usb", ATTRS{idVendor}=="03e7", MODE="0666"' | sudo tee /etc/udev/rules.d/80-movidius.rules
    $ sudo udevadm control --reload-rules && sudo udevadm trigger

Now, you should be able to start using the demo script, which we will do now

Run demo script
###############

Having everything set up, we are now ready to use the demo script by running

.. code-block:: bash

  $ python3 depthai_demo.py

This will compile and download a default `mobilenet-ssd` model, configure the DepthAI and then display
:code:`rgb` window that will contain a scaled preview from the RGB camera from your device.

If you're using OAK-D, it will also display :code:`depth` window, that will show the depth projection calculated from
left & right camera images by DepthAI.


.. image:: https://user-images.githubusercontent.com/5244214/116865569-28daa400-ac0a-11eb-8772-2a46d24640df.png
  :alt: Default run

Change input camera to left/right (OAK-D only)
##############################################

To run the demo script and get a preview from the left camera, run

.. code-block:: bash

  $ python3 depthai_demo.py -cam left

.. image:: https://user-images.githubusercontent.com/5244214/116867083-bcad6f80-ac0c-11eb-9a4c-70fd6c990777.png
  :alt: Run from left

Respectively, to get a preview from the right camera, run

.. code-block:: bash

  $ python3 depthai_demo.py -cam right

.. image:: https://user-images.githubusercontent.com/5244214/116867211-fda58400-ac0c-11eb-9deb-0469a755e1cc.png
  :alt: Run from right

Default model
#############

While the demo was running, you could see the detection results - and if you were standing in front of the camera,
you should see yourself detected as a person with a pretty high probability.

The model that is used by default is a MobileNetv2 SSD object detector trained on the `PASCAL 2007 VOC <http://host.robots.ox.ac.uk/pascal/VOC/voc2007/>`__ classes, which are:

- Person: person
- Animal: bird, cat, cow, dog, horse, sheep
- Vehicle: airplane, bicycle, boat, bus, car, motorbike, train
- Indoor: bottle, chair, dining table, potted plant, sofa, TV/monitor

So give it a try to detect different objects, like bottles or apples

.. image:: https://user-images.githubusercontent.com/5244214/116867984-4447ae00-ac0e-11eb-9ed1-fac37f78634d.png
  :alt: bottles and apples

Or even cats

.. image:: https://user-images.githubusercontent.com/5244214/117653608-e6c6da80-b194-11eb-80c9-2fbb459639cf.png
  :alt: cat

Using other models
##################

We have prepared other models, which you can try and evaluate by simply changing one command line parameter.
To run the demo script with a different model, e.g. :code:`face-detection-retail-0004`, run the following command


.. code-block:: bash

  $ python3 depthai_demo.py -cnn face-detection-retail-0004

Which will allow you to detect human faces, like below


.. image:: https://user-images.githubusercontent.com/5244214/116868791-ba004980-ac0f-11eb-9dcf-36ab2852d08e.png
  :alt: face

You can use :code:`-cnn <name>` flag to change the model that is being run on the DepthAI. Below, there is a list of
models that you can use, having just the demo script downloaded


.. list-table:: Available models
  :widths: 30 50 10 10
  :header-rows: 1
  :align: center

  * - Name
    - Purpose
    - FPS
    - Links
  * - :code:`deeplabv3p_person`
    - People segmentation
    - 22.1
    - :ref:`Usage <deeplabv3p_person>`
  * - :code:`face-detection-adas-0001`
    - Face detection
    - 6.4
    - :ref:`Usage <face-detection-adas-0001>`
  * - :code:`face-detection-retail-0004`
    - Face detection
    - 26.7
    - :ref:`Usage <face-detection-retail-0004>`
  * - :code:`mobilenet-ssd`
    - Object detection (20 classes)
    - 22.3
    - :ref:`Usage <mobilenet-ssd>`
  * - :code:`pedestrian-detection-adas-0002`
    - People detection
    - 5.6
    - :ref:`Usage <pedestrian-detection-adas-0002>`
  * - :code:`person-detection-retail-0013`
    - People detection
    - 9.4
    - :ref:`Usage <person-detection-retail-0013>`
  * - :code:`person-vehicle-bike-detection-crossroad-1016`
    - People, vehicle and bike detection
    - 5.7
    - :ref:`Usage <person-vehicle-bike-detection-crossroad-1016>`
  * - :code:`yolo-v3`
    - Object detection (80 classes)
    - 1.6
    - :ref:`Usage <yolo-v3>`
  * - :code:`tiny-yolo-v3`
    - Object detection (80 classes)
    - 26.2
    - :ref:`Usage <tiny-yolo-v3>`
  * - :code:`vehicle-detection-adas-0002`
    - Vehicle detection
    - 5.5
    - :ref:`Usage <vehicle-detection-adas-0002>`
  * - :code:`vehicle-license-plate-detection-barrier-0106`
    - License plate detection
    - 27.8
    - :ref:`Usage <vehicle-license-plate-detection-barrier-0106>`

.. _deeplabv3p_person:

- :code:`deeplabv3p_person` - Allows to highlight parts of the image where a person is detected

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn deeplabv3p_person

  .. image:: https://user-images.githubusercontent.com/5244214/118824955-90574b80-b8ba-11eb-863a-a7c3f866f71a.png
    :alt: deeplabv3p_person

.. _face-detection-adas-0001:

- :code:`face-detection-adas-0001` - Allows to detect faces on the image (slower)

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn face-detection-adas-0001

  .. image:: https://user-images.githubusercontent.com/5244214/117137299-c8826880-ada9-11eb-89b6-fafc3be0937f.png
    :alt: face-detection-adas-0001

.. _face-detection-retail-0004:

- :code:`face-detection-retail-0004` - Allows to detect faces on the image (faster)

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn face-detection-retail-0004

  .. image:: https://user-images.githubusercontent.com/5244214/117137578-30d14a00-adaa-11eb-9352-b3cfbc9c69d7.png
    :alt: face-detection-retail-0004

.. _mobilenet-ssd:

- :code:`mobilenet-ssd` - Object detector that detects 20 different classes (default)

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn mobilenet-ssd

  .. image:: https://user-images.githubusercontent.com/5244214/116867984-4447ae00-ac0e-11eb-9ed1-fac37f78634d.png
    :alt: mobilenet-ssd

.. _pedestrian-detection-adas-0002:

- :code:`pedestrian-detection-adas-0002` - allows to detect people on the image (slower)

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn pedestrian-detection-adas-0002

  .. image:: https://user-images.githubusercontent.com/5244214/117141406-c969c900-adae-11eb-93b0-f69a2ca31512.png
    :alt: pedestrian-detection-adas-0002

.. _person-detection-retail-0013:

- :code:`person-detection-retail-0013` - allows to detect people on the image (faster)

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn person-detection-retail-0013

  .. image:: https://user-images.githubusercontent.com/5244214/117142161-adb2f280-adaf-11eb-9c83-b7b4aa027093.png
    :alt: person-detection-retail-0013

.. _person-vehicle-bike-detection-crossroad-1016:

- :code:`person-vehicle-bike-detection-crossroad-1016` - allows to detect both people, bikes and vehicles on the image

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn person-vehicle-bike-detection-crossroad-1016

  .. image:: https://user-images.githubusercontent.com/5244214/117144527-4fd3da00-adb2-11eb-89a4-2733cd9a39af.png
    :alt: person-vehicle-bike-detection-crossroad-1016

.. _yolo-v3:

- :code:`yolo-v3` - Object detector that detects 80 different classes (slower)

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn yolo-v3

  .. image:: https://user-images.githubusercontent.com/5244214/117146045-1603d300-adb4-11eb-86d5-4a4d86b58b4e.png
    :alt: yolo-v3

.. _tiny-yolo-v3:

- :code:`tiny-yolo-v3` - Object detector that detects 80 different classes (faster)

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn tiny-yolo-v3

  .. image:: https://user-images.githubusercontent.com/5244214/117146045-1603d300-adb4-11eb-86d5-4a4d86b58b4e.png
    :alt: tiny-yolo-v3

.. _vehicle-detection-adas-0002:

- :code:`vehicle-detection-adas-0002` - allows to detect vehicles on the image

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn vehicle-detection-adas-0002

  .. image:: https://user-images.githubusercontent.com/5244214/117147219-54e65880-adb5-11eb-8089-c38d09a21076.png
    :alt: vehicle-detection-adas-0002

.. _vehicle-license-plate-detection-barrier-0106:

- :code:`vehicle-license-plate-detection-barrier-0106` - allows to detect both vehicle and license plate on the image (only Chineese license plates)

  .. code-block:: bash

    $ python3 depthai_demo.py -cnn vehicle-license-plate-detection-barrier-0106

  .. image:: https://user-images.githubusercontent.com/5244214/117147703-cd4d1980-adb5-11eb-8109-769cc3a2091a.png
    :alt: vehicle-license-plate-detection-barrier-0106

All of the data we use to download and compile a model can be found `here <https://github.com/luxonis/depthai/tree/main/resources/nn>`__.

Using custom models
###################

Let’s assume you want to run a custom model which you downloaded from the model zoo or trained yourself (or both).
In order to prepare your model to be runnable on DepthAI, it has to be compiled into MyriadX blob format - which
is an optimized version of your model, capable of utilizing MyriadX chip as a processing unit.


our demo script, we support a few ways you can run your custom blob, which will be covered below. As an example,
I’ll add a custom face detection network called :code:`custom_model` (substitute with your preferred name)
and run it with the demo script

Compile MyriadX blob
********************

To receive MyriadX blob, the network has to be already in OpenVINO IR format (consisting of :code:`.xml` and :code:`.bin`
files) that will be used for compilation. We won't focus here on how to obtain this representation for your model, but be sure
to check `official OpenVINO conversion guide <https://docs.openvinotoolkit.org/latest/openvino_docs_MO_DG_prepare_model_convert_model_Converting_Model.html>`__.

To convert :code:`custom_model.xml` and :code:`custom_model.bin`, we'll use the `blobconverter cli <https://pypi.org/project/blobconverter/>`__ - our
tool that utilizes `Online MyriadX blob converter <http://luxonis.com:8080/>`__ to perform the conversion.
No local OpenVINO installation is needed in this case, as all of the dependencies are already installed on the server.
If your model is in TensorFlow or Caffe format, you can still use our tool for conversion, just note that
you'll have to use different input flags and sometimes provide a custom model optimizer args (:ref:`Read more <Converting model to MyriadX blob>`)


First, let's install :code:`blobconverter` from `PyPi <https://pypi.org/project/blobconverter/>`__

.. code-block:: bash

  $ python3 -m pip install -U blobconverter

Now, having the :code:`blobconverter` installed, we can compile our IR files with the following command

.. code-block:: bash

  $ python3 -m blobconverter --openvino-xml /path/to/custom_model.xml --openvino-bin /path/to/custom_model.bin

By running this command, :code:`blobconverter` sends a request to the BlobConverter API to perform
a model compilation on provided files. After compilation, the API responds with a :code:`.blob` file and
deletes all source files that were sent with the request.

After a successful compilation, :code:`blobconverter` returns the path to the downloaded blob file.
Since this blob is required by the :code:`depthai` repository, let's move it there

.. code-block:: bash

  $ mkdir <depthai_repo>/resources/nn/custom_model
  $ mv <path_to_blob> <depthai_repo>/resources/nn/custom_model

Configuration
*************

We need to provide some additional configuration for the demo script to run this blob.
The demo script will look for a :code:`custom_model.json` for details on how to configure the pipeline and parse the results.

If your model is based on MobileNetSSD or Yolo, you can use our :code:`detection` output format.
If it's a different type of network, you can use :code:`raw` (default) output format and  provide a custom handler file
to decode and display the NN results.

You can use these configuration examples to customize your :code:`custom_model.json` inside :code:`resources/nn/custom_model` directory

- **MobileNetSSD**

.. code-block:: json

  {
      "nn_config":
      {
          "output_format" : "detection",
          "NN_family" : "mobilenet",
          "confidence_threshold" : 0.5,
          "input_size": "300x300"
      },
      "mappings":
      {
          "labels":
          [
              "unknown",
              "face"
          ]
      }
  }

- **Yolo**

.. code-block:: json

  {
      "nn_config":
      {
          "output_format" : "detection",
          "NN_family" : "YOLO",
          "input_size": "300x300",
          "NN_specific_metadata" :
          {
              "classes" : 80,
              "coordinates" : 4,
              "anchors" : [10,14, 23,27, 37,58, 81,82, 135,169, 344,319],
              "anchor_masks" :
              {
                  "side26" : [1,2,3],
                  "side13" : [3,4,5]
              },
              "iou_threshold" : 0.5,
              "confidence_threshold" : 0.5
          }
      },
      "mappings":
      {
          "labels":
          [
                "unknown",
                "face"
          ]
      }
  }


- **Raw** (see :ref:`Custom handler <Custom handler>` on details how to create :code:`handler.py` file)

.. code-block:: json

  {
      "nn_config": {
          "output_format" : "raw",
          "input_size": "300x300"
      },
      "handler": "handler.py"
  }

Run the demo script
*******************

Having the files in place, we can now run the demo with our custom model

.. code-block:: bash

  $ python3 depthai_demo.py -cnn custom_model

And you should see the output and your NN results displayed (or printed in the console if :code:`raw` was selected and
there is no handler file)

.. image:: https://user-images.githubusercontent.com/5244214/120194749-4ce7d000-c21e-11eb-80f1-86c35080161e.png
  :alt: custom model

Be sure to check the advanced sections below or see :ref:`Next steps <Next steps>`

Custom handler
**************

Custom handler is a file that the demo script will load and execute to parse the NN results. We specify this file with
:code:`handler` config value, specifying a path to the file of preference. It also requires :code:`raw` output format,
since it prevents the script from handling the results itself.

The :code:`handler.py` file should contain two methods - :code:`decode(nn_manager, packet)` and :code:`draw(nn_manager, data, frames)`

.. code-block:: python

  def decode(nn_manager, packet):
    pass

  def draw(nn_manager, data, frames):
    pass

First method, :code:`decode`, is called whenever a NN packet arrives from the pipeline (stored as a :code:`packet` param)
also providing a :code:`nn_manager` object that contains all nn-related info that was used by the script (like input size etc.).
The goal of this function is to decode the received packets from the NN blob into meaningful results that can later be displayed.


Second one, :code:`draw`, is called with the NN results (returned from :code:`decode`), :code:`nn_manager` object and
:code:`frames` array, having :code:`[(<frame_name>, <frame>), (<frame_name>, <frame>), ...]` items. This array will
contain frames that were specified with the :code:`-s/--show` param.
The goal of this function is to draw the decoded results onto received frames.

Below, you can find an example :code:`handle.py` file that decodes and displays MobilenetSSD-based results.

.. code-block:: python

  import cv2
  import numpy as np
  from depthai_helpers.utils import frame_norm


  def decode(nn_manager, packet):
      bboxes = np.array(packet.getFirstLayerFp16())
      bboxes = bboxes.reshape((bboxes.size // 7, 7))
      bboxes = bboxes[bboxes[:, 2] > 0.5]
      labels = bboxes[:, 1].astype(int)
      confidences = bboxes[:, 2]
      bboxes = bboxes[:, 3:7]
      return {
          "labels": labels,
          "confidences": confidences,
          "bboxes": bboxes
      }


  decoded = ["unknown", "face"]


  def draw(nn_manager, data, frames):
      for name, frame in frames:
          if name == nn_manager.source:
              for label, conf, raw_bbox in zip(*data.values()):
                  bbox = frame_norm(frame, raw_bbox)
                  cv2.rectangle(frame, (bbox[0], bbox[1]), (bbox[2], bbox[3]), (255, 0, 0), 2)
                  cv2.putText(frame, decoded[label], (bbox[0] + 10, bbox[1] + 20), cv2.FONT_HERSHEY_TRIPLEX, 0.5, 255)
                  cv2.putText(frame, f"{int(conf * 100)}%", (bbox[0] + 10, bbox[1] + 40), cv2.FONT_HERSHEY_TRIPLEX, 0.5, 255)

With the custom face detection model, using this code we receive the following output

.. image:: https://user-images.githubusercontent.com/5244214/120194166-908e0a00-c21d-11eb-8806-95b1ad9c43f5.png
  :alt: custom model custom handler

We already use this handler mechanism to decode `deeplabv3p_person <https://github.com/luxonis/depthai/blob/main/resources/nn/deeplabv3p_person/handler.py>`__,
that comes as one of the available networks in the demo script to use

On-demand compilation
*********************

Since files in the IR format can be large, and we're both downloading the blob and uploading IR format to the server,
we have incorporated an OpenVINO-like :code:`model.yml` file structure that BlobConverter server uses internally as well.
You can check how this file looks like `in OpenVINO model zoo <https://github.com/openvinotoolkit/open_model_zoo/blob/master/models/intel/face-detection-retail-0004/model.yml>`__
or in `available models in demo script <https://github.com/luxonis/depthai/blob/main/resources/nn/tiny-yolo-v3/model.yml>`__.

This file is used by the `OpenVINO model downloader <https://github.com/openvinotoolkit/open_model_zoo/tree/master/tools/downloader>`__
that is used to download the required files for compilation. In our demo script, we use these files to
provide a URL to the NN source files instead of uploading them along with the source code. It is also useful because on-demand compilation
allows us to use the same configuration while requesting a different amount of MyriadX SHAVE cores.

To download the blob using :code:`model.yml` file, run

.. code-block:: bash

  $ python3 -m blobconverter --raw-config /path/to/model.yml --raw-name custom_model

You can also leave the `model.yml` file inside `resources/nn/<name>` directory. This will make the demo script perform
the conversion for you and run the received blob

.. code-block:: bash

  $ python3 depthai_demo.py -cnn <name>


Next steps
##########

In the previous sections, we learned how to preview basic DepthAI features. From this point, you can explore the DepthAI world further

- **Looking for inspiration?**

  Check our :ref:`Example Use Cases` for ready to use applications that solve a specific problem on DepthAI

- **Want to start coding?**

  Be sure to check `hello world tutorial on API section <https://docs.luxonis.com/projects/api/en/latest/tutorials/hello_world/>`__ for a step-by-step introduction to the API

- **Want to train and deploy a custom model to DepthAI?**

  Visit :ref:`Custom training` page for ready to use Colab notebooks

.. include::  /pages/includes/footer-long.rst
