API Reference
=============

.. module:: dramatiq


Functions
---------

.. autofunction:: get_broker
.. autofunction:: set_broker
.. autofunction:: get_encoder
.. autofunction:: set_encoder


Actors & Messages
-----------------

.. autofunction:: actor
.. autoclass:: Actor
   :members:
.. autoclass:: Message
   :members:

Class-based Actors
^^^^^^^^^^^^^^^^^^

.. autoclass:: GenericActor
   :members:

Message Composition
^^^^^^^^^^^^^^^^^^^

.. autoclass:: group
   :members:
.. autoclass:: pipeline
   :members:

Message Encoders
^^^^^^^^^^^^^^^^

Encoders are used to serialize and deserialize messages over the wire.

.. autoclass:: Encoder
   :members:
.. autoclass:: JSONEncoder
.. autoclass:: PickleEncoder


Brokers
-------

.. autoclass:: Broker
   :members:
.. autoclass:: Consumer
   :members:  __iter__, __next__, ack, nack, close
.. autoclass:: MessageProxy
   :members:
.. autoclass:: dramatiq.brokers.rabbitmq.RabbitmqBroker
   :members:
   :inherited-members:
.. autoclass:: dramatiq.brokers.redis.RedisBroker
   :members:
   :inherited-members:
.. autoclass:: dramatiq.brokers.stub.StubBroker
   :members:
   :inherited-members:


Middleware
----------

Middleware Base Class
^^^^^^^^^^^^^^^^^^^^^

This defines the hooks available for middleware to implement,
and can be subclassed to implement custom middleware.

.. autoclass:: Middleware
   :members:
   :member-order: bysource

.. _default-middleware:

Default Middleware
^^^^^^^^^^^^^^^^^^

The following middleware classes are all enabled by default, with their default settings.

.. autoclass:: dramatiq.middleware.AgeLimit
.. autoclass:: dramatiq.middleware.Callbacks
.. autoclass:: dramatiq.middleware.Pipelines
.. autoclass:: dramatiq.middleware.Retries
.. autoclass:: dramatiq.middleware.ShutdownNotifications
.. autoclass:: dramatiq.middleware.TimeLimit

.. _optional-middleware:

Optional Middleware
^^^^^^^^^^^^^^^^^^^

The following middleware classes are available, but not enabled by default.

.. autoclass:: dramatiq.middleware.AsyncIO
.. autoclass:: dramatiq.middleware.CurrentMessage
   :members: get_current_message
   :member-order: bysource
.. autoclass:: dramatiq.middleware.prometheus.Prometheus

.. py:class:: dramatiq.results.Results
   :no-index:

   Middleware that automatically stores actor results.
   See :class:`dramatiq.results.Results` for details.

Middleware Errors
^^^^^^^^^^^^^^^^^

The class hierarchy for middleware exceptions:

.. code-block:: none

    BaseException
    +-- Exception
    |   +-- dramatiq.middleware.MiddlewareError
    |       +-- dramatiq.middleware.SkipMessage
    +-- dramatiq.middleware.Interrupt
        +-- dramatiq.middleware.Shutdown
        +-- dramatiq.middleware.TimeLimitExceeded


.. autoclass:: dramatiq.middleware.MiddlewareError
.. autoclass:: dramatiq.middleware.SkipMessage
.. autoclass:: dramatiq.middleware.Interrupt
.. autoclass:: dramatiq.middleware.TimeLimitExceeded
.. autoclass:: dramatiq.middleware.Shutdown


Results
-------

Actor results can be stored and retrieved by leveraging result
backends and the results middleware.  Results and result backends are
not enabled by default and you should avoid using them until you have
a really good use case.  Most of the time you can get by with actors
simply updating data in your database instead of using results.

Results Middleware
^^^^^^^^^^^^^^^^^^

.. autoclass:: dramatiq.results.Results
   :members:
   :exclude-members: actor_options, after_process_message, after_skip_message, after_nack

Results Backends
^^^^^^^^^^^^^^^^

.. autoclass:: dramatiq.results.ResultBackend
   :members:
.. autoclass:: dramatiq.results.backends.MemcachedBackend
.. autoclass:: dramatiq.results.backends.RedisBackend
.. autoclass:: dramatiq.results.backends.StubBackend


Rate Limiters
-------------

Rate limiters can be used to determine whether or not an operation can
be run at the current time across many processes and machines by using
a shared storage backend.

Rate Limiters Backends
^^^^^^^^^^^^^^^^^^^^^^

Rate limiter backends are used to store metadata about rate limits.

.. autoclass:: dramatiq.rate_limits.RateLimiterBackend
   :members:
.. autoclass:: dramatiq.rate_limits.backends.MemcachedBackend
.. autoclass:: dramatiq.rate_limits.backends.RedisBackend
.. autoclass:: dramatiq.rate_limits.backends.StubBackend


Limiters
^^^^^^^^

.. autoclass:: dramatiq.rate_limits.RateLimiter
   :members:
.. autoclass:: dramatiq.rate_limits.BucketRateLimiter
.. autoclass:: dramatiq.rate_limits.ConcurrentRateLimiter
.. autoclass:: dramatiq.rate_limits.WindowRateLimiter

Barriers
^^^^^^^^

.. autoclass:: dramatiq.rate_limits.Barrier
   :members:


Workers
-------

.. autoclass:: Worker
   :members:


Errors
------

.. autoclass:: DramatiqError
   :members:
.. autoclass:: BrokerError
   :members:
.. autoclass:: DecodeError
   :members:
.. autoclass:: ActorNotFound
   :members:
.. autoclass:: QueueNotFound
   :members:
.. autoclass:: ConnectionError
   :members:
.. autoclass:: ConnectionClosed
   :members:
.. autoclass:: ConnectionFailed
   :members:
.. autoclass:: RateLimitExceeded
   :members:
.. autoclass:: Retry
   :members:
.. autoclass:: dramatiq.results.ResultError
   :members:
.. autoclass:: dramatiq.results.ResultMissing
   :members:
.. autoclass:: dramatiq.results.ResultTimeout
   :members:
.. autoclass:: dramatiq.results.ResultFailure
   :members:
