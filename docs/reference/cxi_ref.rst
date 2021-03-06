Working with CXI Files
======================

CXIProtocol
-----------

CXI protocol (:class:`pyrost.CXIProtocol`) is a helper class for a :class:`pyrost.STData`
data container, which tells it where to look for the necessary data fields in a CXI
file. The class is fully customizable so you can tailor it to your particular data
structure of CXI file. The protocol consists of the following attributes for each
data field (`data`, `whitefield`, etc.):

* `datatypes` : Data type (`float`, `int`, or `bool`).
* `default_paths` : CXI file path.

.. note::

    You can save protocol to an INI file with :func:`pyrost.CXIProtocol.export_ini`
    and import protocol from INI file with :func:`pyrost.CXIProtocol.import_ini`.

The default protocol can be accessed with :func:`pyrost.CXIProtocol.import_default`. The protocol
is given by:

.. code-block:: ini

    [config]
    float_precision = float64

    [datatypes]
    basis_vectors = float
    data = float
    defocus = float
    defocus_fs = float
    defocus_ss = float
    distance = float
    energy = float
    error_frame = float
    good_frames = int
    m0 = int
    mask = bool
    n0 = int
    phase = float
    pixel_aberrations = float
    pixel_map = float
    pixel_translations = float
    reference_image = float
    roi = int
    translations = float
    wavelength = float
    whitefield = float
    x_pixel_size = float
    y_pixel_size = float

    [default_paths]
    basis_vectors = /entry_1/instrument_1/detector_1/basis_vectors
    data = /entry_1/data_1/data
    defocus = /speckle_tracking/defocus
    defocus_fs = /speckle_tracking/dfs
    defocus_ss = /speckle_tracking/dss
    distance = /entry_1/instrument_1/detector_1/distance
    energy = /entry_1/instrument_1/source_1/energy
    error_frame = /speckle_tracking/error_frame
    good_frames = /frame_selector/good_frames
    m0 = /speckle_tracking/m0
    mask = /speckle_tracking/mask
    n0 = /speckle_tracking/n0
    phase = /speckle_tracking/phase
    pixel_aberrations = /speckle_tracking/pixel_aberrations
    pixel_map = /speckle_tracking/pixel_map
    pixel_translations = /speckle_tracking/pixel_translations
    reference_image = /speckle_tracking/reference_image
    roi = /speckle_tracking/roi
    translations = /entry_1/sample_1/geometry/translations
    wavelength = /entry_1/instrument_1/source_1/wavelength
    whitefield = /speckle_tracking/whitefield
    x_pixel_size = /entry_1/instrument_1/detector_1/x_pixel_size
    y_pixel_size = /entry_1/instrument_1/detector_1/y_pixel_size

CXILoader
---------

CXI file loader class (:class:`pyrost.CXILoader`) uses a protocol to
automatically load all the necessary data fields from a CXI file. Other than
the information provided by a protocol, a loader class requires the following
attributes:

* `policy` : Loading policy for each attribute enlisted in protocol. If it's
  True, the corresponding attribute will be loaded.
* `load_paths` : List of extra CXI file paths, where the loader will look for
  the data field.

.. note::

    You can save loader to an INI file with :func:`pyrost.CXILoader.export_ini`
    and import loader from an INI file with :func:`pyrost.CXILoader.import_ini`.

The default loader can be accessed with :func:`pyrost.CXILoader.import_default`. The loader
is given by:

.. code-block:: ini

    [load_paths]
    good_frames = [/speckle_tracking/good_frames, /frame_selector/good_frames, /process_3/good_frames]
    mask = [/speckle_tracking/mask, /mask_maker/mask, /entry_1/instrument_1/detector_1/mask]
    translations = [/entry_1/sample_1/geometry/translations, /entry_1/sample_1/geometry/translation, /pos_refine/translation, /entry_1/sample_3/geometry/translation]
    whitefield = [/speckle_tracking/whitefield, /process_1/whitefield, /make_whitefield/whitefield, /process_2/whitefield, /process_3/whitefield]

    [policy]
    basis_vectors = True
    data = True
    defocus = True
    defocus_fs = True
    defocus_ss = True
    distance = True
    energy = False
    error_frame = False
    good_frames = True
    m0 = False
    mask = True
    n0 = False
    phase = False
    pixel_aberrations = False
    pixel_map = False
    pixel_translations = False
    reference_image = False
    roi = True
    translations = True
    wavelength = True
    whitefield = False
    x_pixel_size = True
    y_pixel_size = True

.. automodule:: pyrost.cxi_protocol

Contents
--------

.. toctree::
    :maxdepth: 2

    classes/cxi_protocol
    classes/cxi_loader