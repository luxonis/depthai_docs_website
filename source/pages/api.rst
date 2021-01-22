Python API
==========

Please :ref:`install the necessary dependencies <Supported Platforms>` for your
platform by referring to the table below. Once installed you can :ref:`install
the DepthAI library <Install from PyPi>`.

We are constantly striving to improve how we release our software to keep up
with countless platforms and the numerous ways to package it.  If you do not
see a particular platform or package format listed below please reach out to
us on `Discord <https://discord.com/channels/790680891252932659/794255653870370857>`__
or on `Github <https://github.com/luxonis/depthai>`__.

Supported Platforms
###################

We keep up-to-date, pre-compiled, libraries for the following platforms:

============ =========================================== ================================================= ================================================================================
Platform     Instructions                                Tutorial                                          Support
============ =========================================== ================================================= ================================================================================
Windows 10   :ref:`Platform dependencies <Windows>`      `Video tutorial <https://youtu.be/ekopKJfcWiE>`__ `Discord <https://discord.com/channels/790680891252932659/798284448323731456>`__
macOS        :ref:`Platform dependencies <macOS>`        `Video tutorial <https://youtu.be/0RGmmjed3Hc>`__ `Discord <https://discord.com/channels/790680891252932659/798283911989690368>`__
Ubuntu       :ref:`Platform dependencies <Ubuntu>`       `Video tutorial <https://youtu.be/QXeXMaxj4cM>`__ `Discord <https://discord.com/channels/790680891252932659/798302162160451594>`__
Raspberry Pi :ref:`Platform dependencies <Raspberry Pi>` `Video tutorial <https://youtu.be/BpUMT-xqwqE>`__ `Discord <https://discord.com/channels/790680891252932659/798302708070350859>`__
============ =========================================== ================================================= ================================================================================

And the following platforms are also supported by a combination of the community and Luxonis. We plan to have pre-built solutions for Nvidia Jetson and Robot Operating System in Q2 2021:

====================== ================================================================================
Platform               Support
====================== ================================================================================
Fedora                 `Discord <https://discord.com/channels/790680891252932659/798592589905264650>`__
Robot Operating System `Discord <https://discord.com/channels/790680891252932659/795749142793420861>`__
Nvidia Jetson          `Discord <https://discord.com/channels/790680891252932659/795742008119132250>`__
====================== ================================================================================

macOS
*****

.. code-block:: bash

  bash -c "$(curl -fL http://docs.luxonis.com/_static/install_dependencies.sh)"
  
Close and re-open the terminal window after this command.
  
The script also works on M1 Macs, Homebrew being installed under Rosetta 2, as some Python packages are still missing native M1 support.  In case you already have Homebrew installed natively and things don't work, see `here <https://github.com/luxonis/depthai/issues/299#issuecomment-757110966>`__ for some additional troubleshooting steps.

Note that if the video streaming window does not appear consider running the
following:

.. code-block:: bash

    python3 -m pip install opencv-python --force-reinstall --no-cache-dir

See the `Video preview window fails to appear on macOS <https://discuss.luxonis.com/d/95-video-preview-window-fails-to-appear-on-macos>`_ thread on our forum for more information.

Raspberry Pi
***************

.. code-block:: bash

  sudo curl -fL http://docs.luxonis.com/_static/install_dependencies.sh | bash

Ubuntu
******

.. code-block:: bash

  sudo wget -qO- http://docs.luxonis.com/_static/install_dependencies.sh | bash

openSUSE
********

For openSUSE, available `in this official article <https://en.opensuse.org/SDB:Install_OAK_AI_Kit>`__ how to install the OAK device on the openSUSE platform.

Windows
*******

- Right click on Start
- Choose Windows PowerShell (Admin)
- Install Chocolatey package manager (similar to Homebrew for macOS):

.. code-block:: bash

  Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

- Close the PowerShell and then re-open another PowerShell (Admin) by repeating the first two steps.
- Install Python and PyCharm

.. code-block:: bash

  choco install cmake git python pycharm-community -y


Install from PyPi
#################

PyPI
Docker
Podman
VirtualBox
QEMU
apt
rpm
C++

Our packages are distributed `via PyPi <https://pypi.org/project/depthai/>`__, to install it in your environment use

.. code-block:: bash

  python3 -m pip install depthai

For other installation options, see :ref:`other installation options <Other installation methods>`.

Test installation
#################

We have `depthai <https://github.com/luxonis/depthai>`__ repository on our GitHub that contains many helpful examples and
prepared neural networks you can use to make your prototyping faster. It also includes the test script, maintained by
our contributors, that should help you verify if your setup was correct.

First, clone the `depthai <https://github.com/luxonis/depthai>`__ repository and change directory into this repository:

.. code-block:: bash

  git clone https://github.com/luxonis/depthai.git
  cd depthai

Next install the requirements for this repository.
Note that we recommend installing the dependencies in a virtual environment, so that they don't interfere with other Python
tools/environments on your system. 

- For development machines like Mac/Windows/Ubuntu/etc., we recommend the `PyCharm <https://www.jetbrains.com/pycharm/>`__ IDE, as it automatically makes/manages virtual environments for you, along with a bunch of other benefits.  Alternatively, `conda`, `pipenv`, or `virtualenv` could be used directly (and/or with your preferred IDE).  
- For installations on resource-constrained systems, such as the Raspberry Pi or other small Linux systems, we recommend `conda`, `pipenv`, or `virtualenv`.  To set up a virtual environment with `virtualenv`, run `virtualenv venv && source venv/bin/activate`.  

Using a virtual environment (or system-wide, if you prefer), run the following to install the requirements for this example repository:

.. code-block:: bash

  python3 install_requirements.py

Now, run the demo script from within depthai to make sure everything is working:

.. code-block:: bash

  python3 depthai_demo.py

If all goes well a small window video display with overlays for any items for which the class exists in the example
20-class object detector (class list `here <https://github.com/luxonis/depthai/blob/master/resources/nn/mobilenet-ssd/mobilenet-ssd.json#L22>`__).


Run Other Examples
##################

After you have run this demo, you can either run :code:`python3 depthai_demo.py -h` to see other neural networks that by-default can be run.

After checking this out, proceed to:

- Our tutorials, starting with how to use pre-trained neural models from OpenVINO, `HERE <https://docs.luxonis.com/en/latest/pages/tutorials/pretrained_openvino/>`__
- Our experiments `HERE <https://github.com/luxonis/depthai-experiments>`__ to learn more ways to use DepthAI.  

You can also proceed below to learn how to convert your own neural networks to run on DepthAI.  

And we also have online model training below, which shows you how to train and convert models for DepthAI:

- Online ML Training and model Conversion: `HERE <https://github.com/luxonis/depthai-ml-training/tree/master/colab-notebooks>`__ 

Preparing Myriad X blob and configuration file
##############################################

As you can see in `example`_, basic usage of :func:`Device.create_pipeline` method consists of specifying desired output
streams and AI section, where you specify Myriad X blob and it's configuration
file.

In this section, we'll describe how to obtain both :code:`blob_file` and :code:`blob_file_config`.

Obtaining Myriad X blob
***********************

Since we're utilizing Myriad X VPU, your model needs to be compiled (or accurately - optimized and converted) into
the Myriad X blob file, which will be sent to the device and executed.

Easiest way to obtain this blob is to use our `online BlobConverter app <http://69.164.214.171:8083/>`__. It has all
tools needed for compilation so you don't need to setup anything - and you can even download a blob for the model
from `OpenVINO model zoo <https://github.com/openvinotoolkit/open_model_zoo>`__.

If you'd like, you can also compile the blob yourself. You'll need to install `OpenVINO toolkit <https://docs.openvinotoolkit.org/latest/index.html>`__,
then use `Model Optimizer <https://docs.openvinotoolkit.org/latest/openvino_docs_MO_DG_Deep_Learning_Model_Optimizer_DevGuide.html>`__ and `Myriad Compiler <https://docs.openvinotoolkit.org/latest/openvino_inference_engine_tools_compile_tool_README.html#myriad_platform_option>`__
in order to obtain Myriad X blob.
We've documented example usage of these compilers `here <https://github.com/luxonis/depthai#conversion-of-existing-trained-models-into-intel-movidius-binary-format>`__

Creating Blob configuration file
********************************

If configuration file is not provided or :code:`output_format` is set to :code:`raw`, no decoding is done on device and user must do it manually on host side.

Currently there is support to decode :code:`Mobilenet-SSD` and :code:`(tiny-)YOLO-v3` based networks on the device.
For that configuration file is required with network specific parameters.

Example for `tiny-yolo-v3` network:

.. code-block:: json

  {
      "NN_config":
      {
          "output_format" : "detection",
          "NN_family" : "YOLO",
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
              "person",
              "bicycle",
              "car",
              "..."
          ]
      }
  }


* :code:`NN_config` - configuration for the network
    * :code:`output_format`
        * :code:`"detection"` - decoding done on device, the received packet is in :class:`Detections` format
        * :code:`"raw"` - decoding done on host
    * :code:`NN_family` - `"YOLO"` or `"mobilenet"`
    * :code:`NN_specific_metadata` - only for `"YOLO"`
        * :code:`classes` - number of classes
        * :code:`coordinates` - number of coordinates
        * :code:`anchors` - anchors for YOLO network
        * :code:`anchor_masks` - anchor mask for each output layer : :code:`26x26`, :code`13x13` (+ `52x52` for full YOLO-v3)
        * :code:`iou_threshold` - intersection over union threshold for detected object
        * :code:`confidence_threshold` - score confidence threshold for detected object
* :code:`mappings.labels` - used by :code:`depthai_demo.py` script to decode labels from id's

Example decoding when :code:`output_format` is set to :code:`detection`:

.. code-block:: python

  nnet_packets, data_packets = p.get_available_nnet_and_data_packets()

  for nnet_packet in nnet_packets:
    in_layers = nnet_packet.getInputLayersInfo()

    input_width  = in_layers[0].get_dimension(depthai.TensorInfo.Dimension.W)
    input_height = in_layers[0].get_dimension(depthai.TensorInfo.Dimension.H)

    detections = nnet_packet.getDetectedObjects()
    objects = list()

    for detection in detections:
        detection_dict = detection.get_dict()
        # scale normalized coordinates to image coordinates
        detection_dict["x_min"] = int(detection_dict["x_min"] * input_width)
        detection_dict["y_min"] = int(detection_dict["y_min"] * input_height)
        detection_dict["x_max"] = int(detection_dict["x_max"] * input_width)
        detection_dict["y_max"] = int(detection_dict["y_max"] * input_height)
        objects.append(detection_dict)

  print(objects)

Example of decoding for full :code:`yolo-v3` and :code:`tiny-yolo-v3` on host and device is `here <https://github.com/luxonis/depthai/blob/develop/depthai_helpers/tiny_yolo_v3_handler.py>`__


Example of decoding for :code:`mobilenet` based networks on host and device is `here <https://github.com/luxonis/depthai/blob/develop/depthai_helpers/mobilenet_ssd_handler.py>`__


Other installation methods
##########################

To get the latest and yet unreleased features from our source code, you can go ahead and compile depthai package manually.

Dependencies to build from source
*********************************

- CMake > 3.2.0
- Generation tool (Ninja, make, ...)
- C/C++ compiler
- libusb1 development package

.. _raspbian:

Ubuntu, Raspberry Pi OS, ... (Debian based systems)
---------------------------------------------------

On Debian based systems (Raspberry Pi OS, Ubuntu, ...) these can be acquired by running:

.. code-block:: bash

  sudo apt-get -y install cmake libusb-1.0-0-dev build-essential

macOS (Mac OS X)
----------------

Assuming a stock Mac OS X install, `depthai-python <https://github.com/luxonis/depthai-python>`__ library needs following dependencies

- Homebrew (If it's not installed already)

  .. code-block:: bash

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

- Python, :code:`libusb`, CMake, :code:`wget`

  .. code-block:: bash

      brew install coreutils python3 cmake libusb wget

And now you're ready to clone the `depthai-python <https://github.com/luxonis/depthai-python>`__ from Github and build it for Mac OS X.

Install using GitHub commit
***************************

Pip allows users to install the packages from specific commits, even if they are not yet released on PyPi.

To do so, use the command below - and be sure to replace the :code:`<commit_sha>` with the correct commit hash `from here <https://github.com/luxonis/depthai-python/commits>`__

.. code-block:: bash

    python3 -m pip install git+https://github.com/luxonis/depthai-python.git@<commit_sha>

Using/Testing a Specific Branch/PR
**********************************

From time to time, it may be of interest to use a specific branch.  This may occur, for example,
because we have listened to your feature request and implemented a quick implementation in a branch.
Or it could be to get early access to a feature that is soaking in our :code:`develop` for stability purposes before being merged into :code:`main`.

So when working in the `depthai <https://github.com/luxonis/depthai>`__ repository, using a branch can be accomplished
with the following commands.  For this example, the :code:`branch` that we will try out is :code:`develop`
(which is the branch we use to soak new features before merging them into :code:`main`):

Prior to running the following, you can either clone the repository independently
(for not over-writing any of your local changes) or simply do a :code:`git pull` first.

.. code-block:: bash

  git checkout develop
  python3 install_requirements.py

Install from source
*******************

If desired, you can also install the package from the source code itself - it will allow you to make the changes
to the API and see them live in action.

To do so, first download the repository and then add the package to your python interpreter in development mode

.. code-block:: bash

  git clone https://github.com/luxonis/depthai-python.git
  cd depthai-python
  git submodule update --init --recursive
  python3 setup.py develop  # you may need to add sudo if using system interpreter instead of virtual environment

If you want to use other branch (e.g. :code:`develop`) than default (:code:`main`), you can do so by typing

.. code-block:: bash

  git checkout develop  # replace the "develop" with a desired branch name
  git submodule update --recursive
  python3 setup.py develop

Or, if you want to checkout a specific commit, type

.. code-block:: bash

  git checkout <commit_sha>
  git submodule update --recursive
  python3 setup.py develop


API Reference
#############

.. class:: Device

  :canonical: depthai.Device

  Represents the DepthAI device with the methods to interact with it.

  .. warning::

    Please be aware that all methods except :func:`get_available_streams` require :func:`create_pipeline` to be run first,


  .. _example:

  **Example**

  .. code-block:: python

    import depthai
    device = depthai.Device('', False)
    pipeline = device.create_pipeline(config={
        'streams': ['previewout', 'metaout'],
        'ai': {
            "blob_file": "/path/to/model.blob",
            "blob_file_config": "/path/to/config.json",
        },
    })


  **Methods**

  .. function:: __init__(device_id: str, usb2_mode: bool) -> Device

    Standard and recommended way to set up the object.

    **device_id** represents the USB port id that the device is connected to. If set to specific value (e.x. :code:`"1"`) it will
    look for the device in specific USB port, whereas if left empty - :code:`''` - it will look for the device on all ports.
    It's useful when we have more than one DepthAI devices connected and want to specify which one to use in the code

    **usb2_mode**, being :code:`True/False`, allows the DepthAI to communicate using USB2 protocol, not USB3. This lowers the
    throughput of the pipeline, but allows to use >1m USB cables for connection

  .. function:: __init__(cmd_file: str, device_id: str) -> Device
    :noindex:

    Development and debug way to initialize the DepthAI device.

    **cmd_file** is a path to firmware :code:`.cmd` file that will be loaded onto the device for boot.

    **device_id** represents the USB port id that the device is connected to. If set to specific value (e.x. :code:`"1"`) it will
    look for the device in specific USB port, whereas if left empty - :code:`''` - it will look for the device on all ports.
    It's useful when we have more than one DepthAI devices connected and want to specify which one to use in the code

  .. function:: create_pipeline(config: dict) -> depthai.CNNPipeline

    Initializes a DepthAI Pipeline, returning the created :code:`CNNPipeline` if successful and :code:`None` otherwise.

    **config(dict)** -  A :code:`dict` of pipeline configuration settings. Example key/values for the config:

    .. code-block:: python

      {
          # Possible streams:
          #   'color' - 4K color camera preview
          #   'left' - left mono camera preview
          #   'right' - right mono camera preview
          #   'rectified_left' - rectified left camera preview
          #   'rectified_right' - rectified right camera preview
          #   'previewout' - neural network input preview
          #   'metaout' - CNN output tensors
          #   'depth' - the raw depth map, disparity converted to real life distance
          #   'disparity' - disparity map, the disparity between left and right cameras, in pixels
          #   'disparity_color' - disparity map colorized
          #   'meta_d2h' - device metadata stream
          #   'video' - H.264/H.265 encoded color camera frames
          #   'jpegout' - JPEG encoded color camera frames
          #   'object_tracker' - Object tracker results
          'streams': [
              'left',  # if left is used, it must be in the first position
              'right',
              {'name': 'previewout', 'max_fps': 12.0},  # streams can be specified as objects with additional params
              'metaout',
              # depth-related streams
              {'name': 'depth', 'max_fps': 12.0},
              {'name': 'disparity', 'max_fps': 12.0},
              {'name': 'disparity_color', 'max_fps': 12.0},
          ],
          'depth':
          {
              'calibration_file': consts.resource_paths.calib_fpath,
              'left_mesh_file': consts.resource_paths.left_mesh_fpath,
              'right_mesh_file': consts.resource_paths.right_mesh_fpath,
              'padding_factor': 0.3,
              'depth_limit_m': 10.0, # In meters, for filtering purpose during x,y,z calc
              'median_kernel_size': 7,  # Disparity / depth median filter kernel size (N x N) . 0 = filtering disabled
              'lr_check': True  # Enable stereo 'Left-Right check' feature.
              'warp_rectify':
              {
                  'use_mesh' : True, # if False, will use homography
                  'mirror_frame': True, # if False, the disparity will be mirrored instead
                  'edge_fill_color': 0, # gray 0..255, or -1 to replicate pixel values
              },
          },
          'ai':
          {
              'blob_file': blob_file,
              'blob_file_config': blob_file_config,
              'blob_file2': blob_file2,
              'blob_file_config2': blob_file_config2,
              'calc_dist_to_bb': True, # depth calculation on CNN models with bounding box output
              'keep_aspect_ratio': False, # Keep aspect ratio, don't use full RGB FOV for NN
              'camera_input': "left", # 'rgb', 'left', 'right', 'left_right', 'rectified_left', 'rectified_right', 'rectified_left_right'
              'shaves' : 7,  # 1 - 14 Number of shaves used by NN.
              'cmx_slices' : 7,  # 1 - 14 Number of cmx slices used by NN.
              'NN_engines' : 2,  # 1 - 2 Number of NN_engines used by NN.
          },
          # object tracker
          'ot':
          {
              'max_tracklets'        : 20, #maximum 20 is supported
              'confidence_threshold' : 0.5, #object is tracked only for detections over this threshold
          },
          'board_config':
          {
              'swap_left_and_right_cameras': True, # Swap the Left and Right cameras.
              'left_fov_deg': 73.5, # Horizontal field of view (HFOV) for the stereo cameras in [deg].
              'rgb_fov_deg': 68.7938, # Horizontal field of view (HFOV) for the RGB camera in [deg]
              'left_to_right_distance_cm': 9.0, # Left/Right camera baseline in [cm]
              'left_to_rgb_distance_cm': 2.0, # Distance the RGB camera is from the Left camera.
              'store_to_eeprom': False, # Store the calibration and board_config (fov, baselines, swap-lr) in the EEPROM onboard
              'clear_eeprom': False, # Invalidate the calib and board_config from EEPROM
              'override_eeprom': False, # Use the calib and board_config from host, ignoring the EEPROM data if programmed
          },
          'camera':
          {
              'rgb':
              {
                  # 3840x2160, 1920x1080
                  # only UHD/1080p/30 fps supported for now
                  'resolution_h': 3040, # possible - 1080, 2160, 3040
                  'fps': 30,
              },
              'mono':
              {
                  # 1280x720, 1280x800, 640x400 (binning enabled)
                  'resolution_h': 800, # possible - 400, 720, 800
                  'fps': 30,
              },
          },
          'app':
          {
              'sync_video_meta_streams': False,  # Synchronize 'previewout' and 'metaout' streams
              'sync_sequence_numbers'  : False,  # Synchronize sequence numbers for all packets. Experimental
              'usb_chunk_KiB' : 64, # USB transfer chunk on device. Higher (up to megabytes) may improve throughput, or 0 to disable chunking
          },
          #'video_config':
          #{
          #    'rateCtrlMode': 'cbr', # Options: cbr / vbr
          #    'profile': 'h265_main', # Options: 'h264_baseline' / 'h264_main' / 'h264_high' / 'h265_main / 'mjpeg' '
          #    'bitrate': 8000000, # When using CBR (H264/H265 only)
          #    'maxBitrate': 8000000, # When using CBR (H264/H265 only)
          #    'keyframeFrequency': 30, (H264/H265 only)
          #    'numBFrames': 0, (H264/H265 only)
          #    'quality': 80 # (0 - 100%) When using VBR or MJPEG profile
          #}
          #'video_config':
          #{
          #    'profile': 'mjpeg',
          #    'quality': 95
          #}
      }


  .. function:: get_available_streams() -> List[str]

    Return a list of all streams supported by the DepthAI library.

    .. code-block::

      >>> device.get_available_streams()
      ['meta_d2h', 'color', 'left', 'right', 'rectified_left', 'rectified_right', 'disparity', 'depth', 'metaout', 'previewout', 'jpegout', 'video', 'object_tracker']


  .. function:: get_nn_to_depth_bbox_mapping() -> dict

    Returns dict that allows to match the CNN output with the disparity info.

    Since the RGB camera has a 4K resolution and the neural networks accept only images with specific resolution
    (like 300x300), the original image is cropped to meet the neural network requirements.
    On the other side, the disparity frames returned by the neural network are in full resolution available on the mono cameras.

    To be able to determine where the CNN previewout image is on the disparity frame, this method should be used as it
    specifies the offsets and dimensions to use.

    .. code-block::

      >>> device.get_nn_to_depth_bbox_mapping()
      {'max_h': 681, 'max_w': 681, 'off_x': 299, 'off_y': 59}


  .. function:: request_af_mode()

      Set the 4K RGB camera autofocus mode to one of the available :class:`AutofocusMode`


  .. function:: request_af_trigger()

      Manually send trigger action to AutoFocus on 4k RGB camera


  .. function:: request_jpeg()

      Capture a JPEG frame from the RGB camera and send it to :code:`jpegout` stream.
      The frame is in full available resolution, not cropped to meet the CNN input dimensions.


  .. function:: send_disparity_confidence_threshold(confidence: int)

     Function to send disparity confidence threshold for StereoSGBM algorithm.
     If the disparity value confidence is below the threshold, the value is marked as invalid disparity
     and treated as background


  .. function:: get_right_homography()

    .. warning::

      Note: Requires :ref:`dual-homography calibration <Dual-Homography vs. Single-Homography Calibration>`.

     Return a 3x3 homography matrix used to rectify the right stereo camera image.


  .. function:: get_left_homography()

    .. warning::

      Note: Requires :ref:`dual-homography calibration <Dual-Homography vs. Single-Homography Calibration>`.

     Return a 3x3 homography matrix used to rectify the left stereo camera image.


  .. function:: get_left_intrinsic()

    .. warning::

      Note: Requires :ref:`dual-homography calibration <Dual-Homography vs. Single-Homography Calibration>`.

     Return a 3x3 intrinsic calibration matrix of the left stereo camera.


  .. function:: get_right_intrinsic()

    .. warning::

      Note: Requires :ref:`dual-homography calibration <Dual-Homography vs. Single-Homography Calibration>`.

     Return a 3x3 intrinsic calibration matrix of the right stereo camera.


  .. function:: get_rotation()

    .. warning::

      Note: Requires :ref:`dual-homography calibration <Dual-Homography vs. Single-Homography Calibration>`.

     Return a 3x3 rotation matrix representing the rotation of the right stereo camera w.r.t left stereo camera.


  .. function:: get_translation()

    .. warning::

      Note: Requires :ref:`dual-homography calibration <Dual-Homography vs. Single-Homography Calibration>`.

     Return a 3x1 vector representing the position of the right stereo camera center w.r.t left stereo camera center.


.. class:: AutofocusMode

  :canonical: depthai.AutofocusMode


  An enum with all autofocus modes available

  **Members**

  .. attribute:: AF_MODE_AUTO

    This mode sets the Autofocus to a manual mode, where you need to call :func:`Device.request_af_trigger`
    to start focusing procedure.

  .. attribute:: AF_MODE_CONTINUOUS_PICTURE

    This mode adjusts the focus continually to provide the best in-focus image stream and should be used when the
    camera is standing still while capturing. Focusing procedure is done as fast as possible.

    This is the default mode the DepthAI operates in.

  .. attribute:: AF_MODE_CONTINUOUS_VIDEO

    This mode adjusts the focus continually to provide the best in-focus image stream and should be used when the
    camera is trying to capture a smooth video steam. Focusing procedure is slower and avoids focus overshoots

  .. attribute:: AF_MODE_EDOF

    This mode disables the autofocus. EDOF stands for Enhanced Depth of Field and is a digital focus.

  .. attribute:: AF_MODE_MACRO

    It's the same operating mode as :attr:`AF_MODE_AUTO`


.. class:: CNNPipeline

  :canonical: depthai.CNNPipeline

  Pipeline object using which the device is able to send it's result to the host.

  **Methods**

  .. function:: get_available_data_packets() -> List[depthai.DataPacket]

    Returns only data packets produced by the device itself, without CNN results


  .. function:: get_available_nnet_and_data_packets() -> tuple[List[depthai.NNetPacket], List[depthai.DataPacket]]

    Return both neural network results and data produced by device


.. class:: NNetPacket

  :canonical: depthai.NNetPacket

  For any neural network inference output :func:`NNPacket.get_tensor` can be used. For the specific case
  of :code:`Mobilenet-SSD`, :code:`YOLO-v3` decoding can be done in the firmware. Decoded objects can be accessed
  through :func:`getDetectedObjects` as well in addition to raw output to make the results of this commonly used
  networks easily accessible. See :ref:`blob config file <Creating Blob configuration file>` for more details about
  different neural network output formats and how to choose between these formats.

  Neural network results packet. It's not a single result, but a batch of results with additional metadata attached

  **Methods**

  .. function:: getMetadata() -> depthai.FrameMetadata

    Returns metadata object containing all proprietary data related to this packet


  .. function:: get_tensor(name: Union[int, str]) -> numpy.ndarray

    .. warning::

      Works only, when in :ref:`blob config file <Creating Blob configuration file>` :code:`output_format` is set to :code:`raw`.

    Returns a shaped numpy array for the specific network output tensor, based on the neural network's output layer information.

    For example: in case of :code:`Mobilenet-SSD` it returns a :code:`[1, 1, 100, 7]` shaped array, where :code:`numpy.dtype` is :code:`float16`.

    Example of usage:

    .. code-block::

      nnetpacket.get_tensor(0)
      # or
      nnetpacket.get_tensor('detection_out')

  .. function:: __getitem__(name: Union[int, str]) -> numpy.ndarray

    Same as :func:`get_tensor`

    Example of usage for :code:`Mobilenet-SSD`:

    .. code-block::

      nnetpacket[0]
      # or
      nnetpacket['detection_out']

  .. function:: getOutputsList() -> list

    Returns all the output tensors in a list for the network.

  .. function:: getOutputsDict() -> dict

    Returns all the output tensors in a dictionary for the network.
    The key is the name of the output layer, the value is the shaped numpy array.

  .. function:: getOutputLayersInfo() -> depthai.TensorInfo

    Returns information about the output layer for the network.

  .. function:: getInputLayersInfo() -> depthai.TensorInfo

    Returns information about the input layers for the network.

  .. function:: getDetectedObjects() -> depthai.Detections

    .. warning::

      Works when in :ref:`blob config file <Creating Blob configuration file>` :code:`output_format` is set to :code:`detection` and with detection networks
      (:code:`Mobilenet-SSD`, :code:`(tiny-)YOLO-v3` based networks)

    Returns the detected objects in :class:`Detections` format. The network is decoded on device side.


.. class:: TensorInfo

  :canonical: depthai.TensorInfo

  Descriptor of the input/output layers/tensors of the network.

  When network is loaded the tensor info is automatically printed.

  **Attributes**

  .. attribute:: name
    :type: str

    Name of the tensor.

  .. attribute:: dimensions
    :type: list

    Shape of tensor array. E.g. : :code:`[1, 1, 100, 7]`

  .. attribute:: strides
    :type: list

    Strides of tensor array.

  .. attribute:: data_type
    :type: string

    Data type of tensor. E.g. : :code:`float16`

  .. attribute:: offset
    :type: int

    Offset in the raw output array.

  .. attribute:: element_size
    :type: int

    Size in bytes of one element in the array.

  .. attribute:: index
    :type: int

    Index of the tensor. E.g. : in case of multiple inputs/outputs in the network it marks the order of input/output.

  **Methods**

  .. function:: get_dict() -> dict

    Returns TensorInfo in a dictionary where the `key` is the name of attribute.

  .. function:: get_dimension() -> int

    Returns the specific dimension of the tensor

    .. code-block::

      tensor_info.get_dimension(depthai.TensorInfo.Dimension.WIDTH)  # returns width of tensor


.. class:: Detections

  :canonical: depthai.Detections

  Container of neural network results decoded on device side.

  **Example of accessing detections**

  Assuming the detected objects are stored in :code:`detections` object.

  * Number of detections

    .. code-block::

      detections.size()
      # or
      len(detections)

  * Accessing the nth detection

    .. code-block::

      detections[0]
      detections[1]  # ...

  * Iterating through all detections

    .. code-block::

      for detection in detections:


.. class:: Detection

  :canonical: depthai.Detection

  Detected object descriptor.

  **Attributes**

  .. attribute:: label
    :type: int

    Label id of the detected object.

  .. attribute:: confidence
    :type: float

    Confidence score of the detected object in interval [0, 1].

  .. attribute:: x_min
    :type: float

    Top left :code:`X` coordinate of the detected bounding box. Normalized, in interval [0, 1].

  .. attribute:: y_min
    :type: float

    Top left :code:`Y` coordinate of the detected bounding box. Normalized, in interval [0, 1].

  .. attribute:: x_max
    :type: float

    Bottom right :code:`X` coordinate of the detected bounding box. Normalized, in interval [0, 1].

  .. attribute:: y_max
    :type: float

    Bottom right :code:`Y` coordinate of the detected bounding box. Normalized, in interval [0, 1].

  .. attribute:: depth_x
    :type: float

    Distance to detected bounding box on :code:`X` axis. Only when depth calculation is enabled (stereo cameras are present on board).

  .. attribute:: depth_y
    :type: float

    Distance to detected bounding box on :code:`Y` axis. Only when depth calculation is enabled (stereo cameras are present on board).

  .. attribute:: depth_z
    :type: float

    Distance to detected bounding box on :code:`Z` axis. Only when depth calculation is enabled (stereo cameras are present on board).

  **Methods**

  .. function:: get_dict() -> dict

    Returns detected object in a dictionary where the :code:`key` is the name of attribute.


.. class:: Dimension

  :canonical: depthai.TensorInfo.Dimension

  Dimension descriptor of tensor shape. Mostly meaningful for input tensors since not all neural network models
  respect the semantics of :code:`Dimension` for output tensor


  **Values**

  .. attribute:: W / WIDTH
    :type: str

    Width

  .. attribute:: H / HEIGHT
    :type: str

    Height

  .. attribute:: C / CHANNEL
    :type: str

    Number of channels

  .. attribute:: N / NUMBER
    :type: str

    Number of inferences

  .. attribute:: B / BATCH
    :type: str

    Batch of inferences


.. class:: DataPacket

  :canonical: depthai.DataPacket

  DepthAI data packet, containing information generated on the device. Unlike NNetPacket, it contains a single "result"
  with source stream info

  **Attributes**

  .. attribute:: stream_name
    :type: str

    Returns packet source stream. Used to determine the origin of the packet and therefore allows to handle the packets
    correctly, applying proper handling based on this value

  **Methods**

  .. function:: getData() -> numpy.ndarray

    Returns the data as NumPy array, which you can be further transformed or displayed using OpenCV :code:`imshow`.

    Used with streams that returns frames e.x. :code:`previewout`, :code:`left`, :code:`right`, or encoded data e.x. :code:`video`, :code:`jpegout`.

  .. function:: getDataAsStr() -> str

    Returns the data as a string, capable to be parsed further.

    Used with streams that returns non-array results e.x. :code:`meta_d2h` which returns JSON object

  .. function:: getMetadata() -> FrameMetadata

    Returns metadata object containing all proprietary data related to this packet

  .. function:: getObjectTracker() -> ObjectTracker

    .. warning::

      Works only with packets from :code:`object_tracker` stream

    Returns metadata object containing :class:`ObjectTracker` object

  .. function:: size() -> int

    Returns packet data size


.. class:: FrameMetadata

  :canonical: depthai.FrameMetadata

  Metadata object attached to the packets sent via pipeline.

  **Methods**

  .. function:: getCameraName() -> str

    Returns the name of the camera that produced the frame.

  .. function:: getCategory() -> int

    Returns the type of the packet, whether it's a regular frame or arrived from taking a still

  .. function:: getFrameBytesPP() -> int

    Returns number of bytes per pixel in the packet's frame

  .. function:: getFrameHeight() -> int

    Returns the height of the packet's frame

  .. function:: getFrameWidth() -> int

    Returns the width of the packet's frame

  .. function:: getFrameType() -> int

    Returns the type of the data that this packet contains.

  .. function:: getInstanceNum() -> int

    Returns the camera id that is the source of the current packet

  .. function:: getSequenceNum() -> int

    Sequence number is assigned for each frame produced by the camera.
    It can be used to assure the frames are captured at the same time - e.x. if frames from left and right camera have
    the same sequence number, you can assume they were taken at the same time

  .. function:: getStride() -> int

    Specifies number of bytes till the next row of pixels in the packet's frame

  .. function:: getTimestamp() -> float

    When packet is created, it is assigned a creation timestamp, which can be obtained using this method


.. class:: ObjectTracker

  :canonical: depthai.ObjectTracker

  Object representing current state of the tracker, obtained by calling :func:`DataPacket.getObjectTracker`
  method on a packet from :code:`object_tracker` stream

  **Methods**

  .. function:: getNrTracklets() -> int

    Return the number of available tracklets

  .. function:: getTracklet(tracklet_nr: int) -> Tracklet

    Returns the tracklet with specified :code:`tracklet_nr`.
    To check how many tracklets there are, please use :func:`getNrTracklets` method


.. class:: Tracklet

  :canonical: depthai.Tracklet

  Tracklet is representing a single tracked object, is produced by :class:`ObjectTracker` class.
  To obtain it, call :func:`ObjectTracker.getTracklet` method.

  **Methods**

  .. function:: getId() -> int

    Return the tracklet id

  .. function:: getLabel() -> int

    Return the tracklet label, being the neural network returned result. Used to identify a class of recognized objects

  .. function:: getStatus() -> str

    Return the tracklet status - either :code:`NEW`, :code:`TRACKED`, or :code:`LOST`.

  .. function:: getLeftCoord() -> int

    Return the left coordinate of the bounding box of a tracked object

  .. function:: getRightCoord() -> int

    Return the right coordinate of the bounding box of a tracked object

  .. function:: getTopCoord() -> int

    Return the top coordinate of the bounding box of a tracked object

  .. function:: getBottomCoord() -> int

    Return the bottom coordinate of the bounding box of a tracked object

.. include::  /pages/includes/footer-short.rst

..
  Below you can see ?dummy=http://, this is a workaround for a Sphinx, see here - https://github.com/sphinx-doc/sphinx/issues/701#issuecomment-697116337

.. toctree::
   :maxdepth: 1
   :hidden:
   :caption: Contents:

   depthai.Device <?dummy=http://#Device>
   depthai.AutofocusMode <?dummy=http://#AutofocusMode>
   depthai.CNNPipeline <?dummy=http://#CNNPipeline>
   depthai.NNetPacket <?dummy=http://#NNetPacket>
   depthai.TensorInfo <?dummy=http://#TensorInfo>
   depthai.Detections <?dummy=http://#Detections>
   depthai.Dimension <?dummy=http://#Dimension>
   depthai.DataPacket <?dummy=http://#DataPacket>
   depthai.FrameMetadata <?dummy=http://#FrameMetadata>
   depthai.ObjectTracker <?dummy=http://#ObjectTracker>
   depthai.Tracklet <?dummy=http://#Tracklet>
