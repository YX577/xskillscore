=================
Changelog History
=================

xskillscore v0.0.19 (2020-XX-XX)
--------------------------------

Features
~~~~~~~~
- Added mean error
  :py:func:`~xskillscore.me`. (:issue:`202`, :pr:`200`)
  `Andrew Huang`_
- Added MAE significance test :py:func:`~xskillscore.mae_test` from Jolliffe and Ebert
  https://www.cawcr.gov.au/projects/verification/CIdiff/FAQ-CIdiff.html
  (:issue:`192`, :pr:`209`) `Aaron Spring`_
- :py:func:`~xskillscore.resampling.resample_iterations` and faster
  :py:func:`~xskillscore.resampling.resample_iterations_idx` for resampling with and
  without replacement. (:issue:`215`, :pr:`225`) `Aaron Spring`_

Breaking changes
~~~~~~~~~~~~~~~~
- Aligned output of :py:func:`~xskillscore.sign_test` with
  :py:func:`~xskillscore.mae_test`. Now tests from comparative.py return more than
  one object including a boolean indicating ``signficance`` based on ``alpha``.
  (:pr:`209`) `Aaron Spring`_

Bug Fixes
~~~~~~~~~
- :py:func:`~xskillscore.sign_test` now works for ``xr.Dataset`` inputs.
  (:issue:`198`, :pr:`199`) `Aaron Spring`_

Internal Changes
~~~~~~~~~~~~~~~~
- Added Python 3.7 and Python 3.8 to the CI. Use the latest version of Python 3
  for development. (:issue:`21`, :pr:`189`). `Aaron Spring`_
- Lint with the latest black. (:issue:`179`, :pr:`191`). `Ray Bell`_


xskillscore v0.0.18 (2020-09-23)
--------------------------------

Features
~~~~~~~~
- Added the sign test described in DelSole and Tippett 2016:
  :py:func:`~xskillscore.sign_test`. (:issue:`133`, :pr:`176`)
  `Aaron Spring`_ and `Dougie Squire`_

Internal Changes
~~~~~~~~~~~~~~~~
- Removed an unused variable in ``_rmse``, resulting in 2x speedup
  (:pr:`182`). `Andrew Huang`_
- Require ``xarray=0.16.1`` (:issue:`183`, :pr:`184`) `Aaron Spring`_

Bug Fixes
~~~~~~~~~
- Fix incompatibility with ``xarray=0.16.1`` in ``apply_ufunc``
  (:issue:`183`, :pr:`184`) `Aaron Spring`_

Documentation
~~~~~~~~~~~~~
- Added ``CONTRIBUTING.md`` to trigger built-in Github
  contribution guide reference (:pr:`181`) `mcsitter`_.


xskillscore v0.0.17 (2020-09-06)
--------------------------------

Features
~~~~~~~~
- Added contingency table :py:func:`~xskillscore.Contingency` and associated metrics
  (:pr:`119`, :pr:`153`). `Dougie Squire`_
- Added :py:func:`~xskillscore.rank_histogram` and :py:func:`~xskillscore.discrimination`
  to probabilistic metrics (:pr:`136`). `Dougie Squire`_
- Added :py:func:`~xskillscore.reliability` to probabilistic metrics (:pr:`164`). `Dougie Squire`_
- Added ``dim`` and ``weights`` kwargs for probabilistic metrics. (:pr:`121`) `Aaron Spring`_
- Added ``keep_attrs`` kwarg for all metrics. (:pr:`122`) `Andrew Huang`_
- Added ranked probability score :py:func:`~xskillscore.rps`. (:pr:`163`) `Aaron Spring`_
- Deterministic metrics now automatically broadcast any non-core dimensions. E.g., a single
  time series can be compared to a gridded product spanning that same time span.
  (:issue:`165`, :issue:`71`, :issue:`156`, :pr:`166`) `Aaron Spring`_

Breaking Changes
~~~~~~~~~~~~~~~~
- Renamed ``dim`` to ``member_dim`` in probabilistic metrics. (:pr:`121`) `Aaron Spring`_
- Argument ``dim`` becomes keyword ``dim=None`` in all metrics.
  (:issue:`137`, :pr:`143`) `Aaron Spring`_
- ``dim=None`` reduces all dimensions as in ``xr.mean(dim=None)``.
  (:issue:`137`, :pr:`143`) `Aaron Spring`_

Bug Fixes
~~~~~~~~~
- Fixes ``weights=None`` type issue with latest version of ``dask``.
  (:issue:`168`, :pr:`171`) `Andrew Huang`_

Documentation
~~~~~~~~~~~~~
- Added ``sphinx`` documentation with full API and a `quick start <quick-start.html>`__ notebook.
  (:pr:`127`) `Riley X. Brady`_ and `Ray Bell`_.

Internal Changes
~~~~~~~~~~~~~~~~
- Added ``utils`` module to house utilities shared across multiple modules
  (:pr:`119`). `Dougie Squire`_
- Added ``conftest.py`` to gather all ``pytest.fixtures``. (:issue:`126`, :pr:`159`).
  `Aaron Spring`_ and `Ray Bell`_
- Removed ``test_np_deterministic`` covered by ``test_metric_results_accurate``.
  (:pr:`159`) `Aaron Spring`_


xskillscore v0.0.16 (2020-07-18)
--------------------------------

Internal Changes
~~~~~~~~~~~~~~~~
- Add community support documents: ``HOWTOCONTRIBUTE.rst``, issue template and pull request
  template. `Aaron Spring`_ and `Ray Bell`_
- Replace ``pandas`` with ``cftime`` in examples and tests. `Aaron Spring`_ and `Ray Bell`_
- Add coveralls for tests coverage. `Aaron Spring`_ and `Ray Bell`_
- Add ``black``, ``flake8``, ``isort``, ``doc8`` and ``pre-commit`` for formatting
  similar to ``climpred``. `Aaron Spring`_ and `Ray Bell`_

Bug Fixes
~~~~~~~~~
- Avoid mutating inputted arrays when `skipna=True`. (:pr:`111`) `Riley X. Brady`_.
- Avoid read-only error that appeared due to not copying input arrays when dealing
  with NaNs. (:pr:`111`) `Riley X. Brady`_.


xskillscore v0.0.15 (2020-03-24)
--------------------------------

Features
~~~~~~~~
- Update the ``XSkillScoreAccessor`` with all metrics. `Ray Bell`_


xskillscore v0.0.14 (2020-03-20)
--------------------------------

Features
~~~~~~~~
- Add ``r2`` as an implementation of ``sklearn.metrics.r2_score``. `Ray Bell`_


xskillscore v0.0.13 (2020-03-17)
--------------------------------

Bug Fixes
~~~~~~~~~
- Fixes https://github.com/xarray-contrib/xskillscore/issues/79 `assignment destination is read-only`
  error when ``skipna=True`` and weights are passed. `Andrew Huang`_


xskillscore v0.0.12 (2020-01-09)
--------------------------------

Internal Changes
~~~~~~~~~~~~~~~~
- ~30-50% speedup for deterministic metrics when ``weights=None``. `Aaron Spring`_


xskillscore v0.0.11 (2020-01-06)
--------------------------------

Features
~~~~~~~~
- Add ``effective_sample_size``, ``pearson_r_eff_p_value``, and ``spearman_r_eff_p_value``
  for computing statistical significance for temporally correlated data with
  autocorrelation. `Riley X. Brady`_


xskillscore v0.0.10 (2019-12-21)
--------------------------------

Deprecations
~~~~~~~~~~~~
- ``mad`` no longer works and is replaced by ``median_absolute_error``. `Riley X. Brady`_


Bug Fixes
~~~~~~~~~
- ``skipna`` for ``pearson_r`` and ``spearman_r`` and their p-values now reports
  accurate results when there are pairwise nans (i.e., nans that occur in different
  indices in ``a`` and ``b``) `Riley X. Brady`_


Testing
~~~~~~~
- Test that results from grid cells in a gridded product match the same value if their time
  series were input directly into functions. `Riley X. Brady`_
- Test that metric results from ``xskillscore`` are the same value as an external package
  (e.g. ``numpy``, ``scipy``, ``sklearn``). `Riley X. Brady`_
- Test that ``skipna=True`` works properly with pairwise nans. `Riley X. Brady`_


.. _`Aaron Spring`: https://github.com/aaronspring
.. _`Andrew Huang`: https://github.com/ahuang11
.. _`Dougie Squire`: https://github.com/dougiesquire
.. _`mcsitter`: https://github.com/mcsitter
.. _`Riley X. Brady`: https://github.com/bradyrx
.. _`Ray Bell`: https://github.com/raybellwaves
