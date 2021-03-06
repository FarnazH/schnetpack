.. _train model:

Train a model with SchNetPack
=============================

The recommended way to train a model on a dataset is to use the provided
sacred scripts. A general guide to sacred can be found at section
:ref:`sacred basics`. The command to train a model is::

    $ spk_train.py with model_dir=tutorials/model_dir dataset.db_path=tutorials/ethanol.db device=cpu scheduling.reduce_on_plateau dataset.property_mapping='energy:energy'


This will automatically download the specified dataset, train a SchNet model
and use 80% of the data for training, 10% of the data for validation and the remaining
10% for testing.
Furthermore a new directory will be created at the location that you have defined
with the ``model_dir`` argument.
The new directory is used to store checkpoints, logging files and your best model of
the training session.
By setting the ``schedule_hooks`` to ``reduce_on_plateau`` the learning rate will
automatically decrease during training, if the training does not improve any further.
For a detailed view on the possible parameters run::

    $ spk.train.py print_config

Selecting the Dataset
--------------------

You can either use your own datasets, as described in the example above, or
use one of the pre-implemented datasets. These datasets will be downloaded
and preprocessed automatically. In order to use the pre-implemented datasets,
replace ``dataset.db_path`` and ``dataset.property_mapping`` with
``dataset.<name>``. Available datasets are QM9 (as ``qm9``), ISO17 (as
``iso17``),
ANI1 (as ``ani1``), MD17 (as ``md17``) and Materials Project (as ``matproj``).
In order to use your own data you must provide it as an ``ase db`` file.
Visit :ref:`Prepare Data` for additional information on the requirements for
your dataset. After preparing your data use ``dataset.dbpath=<path>`` instead
of choosing a pre-implemented dataset. Additionally you will need to define a
``property_mapping`` in order to connect the model properties to the dataset
properties. Therefore add
``dataset.property_mapping="model_property1:data_property1,..."`` to your run
arguments.


Monitoring Training with TensorBoard
------------------------------------

The default training session will store TensorBoard files for monitoring your
training session in *model_dir/log*. In order to use
TensorBoard open a new terminal and run::

    $ tensorboard --logdir model_dir/log

This will return the url of your TensorBoard. Paste the url to your browser and
your training session will show up.


