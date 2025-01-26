[![Pylint](https://github.com/gaspardpetit/uniscripts/actions/workflows/pylint.yml/badge.svg)](https://github.com/gaspardpetit/uniscripts/actions/workflows/pylint.yml)
[![Python package](https://github.com/gaspardpetit/uniscripts/actions/workflows/python-package.yml/badge.svg)](https://github.com/gaspardpetit/uniscripts/actions/workflows/python-package.yml)
[![PyPI version](https://badge.fury.io/py/uniscripts.svg)](https://pypi.python.org/pypi/uniscripts/)
[![Python versions](https://img.shields.io/pypi/pyversions/uniscripts.svg)](https://pypi.org/project/uniscripts/)
[![Unicode versions](https://img.shields.io/badge/Unicode%20-15.1-blue.svg)](https://www.unicode.org/charts/)
[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](http://creativecommons.org/publicdomain/zero/1.0/)

# Uniscripts

Simple Python 3 module to query Unicode UCD script metadata (see UAX #24).

This module is useful for querying if a text is made of Latin characters,
Arabic, hiragana, kanji (han), and so on.  It works for all scripts supported
by the Unicode character database.

Sample usage:

### Verify is a string is of a given script:

```python
>>> from uniscripts import is_script, Scripts

>>> is_script('A', Scripts.LATIN)
True

# if you pass it a string, all characters must match
>>> is_script('はるはあけぼの', Scripts.HIRAGANA)
True

>>> is_script('はるはAkebono', Scripts.HIRAGANA)
False

# ...but by default, it ignores 'Common' characters, such as punctuation.
>>> is_script('はるは:あけぼの', Scripts.HIRAGANA)
True

>>> is_script('中華人民共和国', Scripts.HAN) # 'Han' = kanji or hànzì
True

```
See docstrings for `is_script()`.


### Detect the script of a character:

```python
>>> from uniscripts import which_scripts

>>> which_scripts('z')
['Latin']

>>> which_scripts('は')
['Hiragana']

>>> which_scripts('ー') # U+30FC
['Bopomofo', 'Common', 'Han', 'Hangul', 'Hiragana', 'Katakana', 'Yi']

```
See docstrings for `is_script()`.


### Detect the script of a text

```python
>>> from uniscripts import get_scripts
>>> sorted(get_scripts("こんにちは"))
['Hiragana']

>>> sorted(get_scripts("チョコレート"))
['Bopomofo', 'Common', 'Han', 'Hangul', 'Hiragana', 'Katakana', 'Yi']

>>> sorted(get_scripts("ਚਾਕਲੇਟ"))
['Gurmukhi']

>>> sorted(get_scripts("초콜릿"))
['Hangul']

>>> sorted(get_scripts("σοκολάτα"))
['Greek']

>>> sorted(get_scripts("شوكولاتة"))
['Arabic']

>>> sorted(get_scripts("chocolat"))
['Common', 'Latin']

```

See docstrings for `get_scripts()`.

### Get the count of characters in each script

```python
>>> from uniscripts import get_script_counts

>>> get_script_counts("こんにちは")
{'Hiragana': 5}

>>> get_script_counts("チョコレート")
{'Bopomofo': 1, 'Common': 1, 'Han': 1, 'Hangul': 1, 'Hiragana': 1, 'Katakana': 1, 'Yi': 1}

>>> get_script_counts("ਚਾਕਲੇਟ")
{'Gurmukhi': 6}

>>> get_script_counts("초콜릿")
{'Hangul': 4}

>>> get_script_counts("σοκολάτα")
{'Greek': 8}

>>> get_script_counts("شوكولاتة")
{'Arabic': 8}

>>> get_script_counts("chocolat")
{'Common': 1, 'Latin': 8}

```

See docstrings for `get_script_counts()`.