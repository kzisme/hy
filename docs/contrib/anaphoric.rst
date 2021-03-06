====================
Anaphoric Macros
====================

The anaphoric macros module makes functional programming in Hy very
concise and easy to read.

    An anaphoric macro is a type of programming macro that
    deliberately captures some form supplied to the macro which may be
    referred to by an anaphor (an expression referring to another).

    -- Wikipedia (http://en.wikipedia.org/wiki/Anaphoric_macro)

Macros
======

.. _ap-each:

ap-each
-------

Usage: ``(ap-each [1 2 3 4 5] (print it))``

Evaluate the form for each element in the list for side-effects.


.. _ap-each-while:

ap-each-while
=============

Usage: ``(ap-each-while list pred body)``

Evaluate the form for each element where the predicate form returns
True.

.. code-block:: clojure

   => (ap-each-while [1 2 3 4 5 6] (< it 4) (print it))
   1
   2
   3

.. _ap-map:

ap-map
======

Usage: ``(ap-map form list)``

The anaphoric form of map works just like regular map except that
instead of a function object it takes a Hy form. The special name,
``it`` is bound to the current object from the list in the iteration.

.. code-block:: clojure

    => (list (ap-map (* it 2) [1 2 3]))
    [2, 4, 6]


.. _ap-map-when:

ap-map-when
===========

Usage: ``(ap-map-when predfn rep list)``

Evaluate a mapping over the list using a predicate function to
determin when to apply the form.

.. code-block:: clojure

    => (list (ap-map-when odd? (* it 2) [1 2 3 4]))
    [2, 2, 6, 4]

    => (list (ap-map-when even? (* it 2) [1 2 3 4]))
    [1, 4, 3, 8]


.. _ap-filter:

ap-filter
=========

Usage: ``(ap-filter form list)``

As with ``ap-map`` we take a special form instead of a function to
filter the elements of the list. The special name ``it`` is bound to
the current element in the iteration.

.. code-block:: clojure

    => (list (ap-filter (> (* it 2) 6) [1 2 3 4 5]))
    [4, 5]


