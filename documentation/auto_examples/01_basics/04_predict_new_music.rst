
.. DO NOT EDIT.
.. THIS FILE WAS AUTOMATICALLY GENERATED BY SPHINX-GALLERY.
.. TO MAKE CHANGES, EDIT THE SOURCE PYTHON FILE:
.. "auto_examples/01_basics/04_predict_new_music.py"
.. LINE NUMBERS ARE GIVEN BELOW.

.. only:: html

    .. note::
        :class: sphx-glr-download-link-note

        Click :ref:`here <sphx_glr_download_auto_examples_01_basics_04_predict_new_music.py>`
        to download the full example code

.. rst-class:: sphx-glr-example-title

.. _sphx_glr_auto_examples_01_basics_04_predict_new_music.py:


4. Predict New Music
====================

In this example we are gonna see how we can use the predict module to extends an already existing chord progression
- We will create a small chord progression
- We will use an already trained WindowedPredictor to predict the next three chords of our song

.. GENERATED FROM PYTHON SOURCE LINES 10-37

.. code-block:: default



    from musiclang.predict.predictors import WindowedPredictor
    from musiclang.predict.tokenizers import ChordTokenizer, ChordDetokenizer
    from musiclang.write.library import *


    tokenizer = ChordTokenizer()
    print('loading model')
    predictor = WindowedPredictor.load('../data/model.pickle')

    chord_progression = (I % I.M) + (VI['6'] % I.M) + (II['2'] % I.M)
    # Tokenize the chord progression
    tokens = tokenizer.tokenize(chord_progression)

    # Predict next two chords
    for i in range(10):
        predicted_token = predictor.predict(tokens)
        tokens.append(predicted_token)

    print(tokens)
    # Convert tokens to a score
    detokenizer = ChordDetokenizer()
    score = detokenizer.detokenize(tokens)
    print(score)
    score.to_voicings().show('midi')



.. rst-class:: sphx-glr-timing

   **Total running time of the script:** ( 0 minutes  0.000 seconds)


.. _sphx_glr_download_auto_examples_01_basics_04_predict_new_music.py:

.. only:: html

  .. container:: sphx-glr-footer sphx-glr-footer-example


    .. container:: sphx-glr-download sphx-glr-download-python

      :download:`Download Python source code: 04_predict_new_music.py <04_predict_new_music.py>`

    .. container:: sphx-glr-download sphx-glr-download-jupyter

      :download:`Download Jupyter notebook: 04_predict_new_music.ipynb <04_predict_new_music.ipynb>`


.. only:: html

 .. rst-class:: sphx-glr-signature

    `Gallery generated by Sphinx-Gallery <https://sphinx-gallery.github.io>`_
