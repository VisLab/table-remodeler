Core components
===============

Core classes for managing remodeling operations, backups, and validation.

Dispatcher
----------

The main orchestrator for executing remodeling operations.

.. autoclass:: remodeler.dispatcher.Dispatcher
   :members:
   :undoc-members:
   :show-inheritance:

BackupManager
-------------

Manages dataset backups before and during remodeling operations.

.. autoclass:: remodeler.backup_manager.BackupManager
   :members:
   :undoc-members:
   :show-inheritance:

RemodelerValidator
------------------

Validates remodeling operation specifications against JSON schema.

.. autoclass:: remodeler.remodeler_validator.RemodelerValidator
   :members:
   :undoc-members:
   :show-inheritance:
