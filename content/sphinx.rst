Sphinx
======

http://sphinx-doc.org/

    "The focus is on hand-written documentation, rather than auto-generated API
    docs. Though there is support for that kind of docs as well (which is
    intended to be freely mixed with hand-written content), if you need pure
    API docs have a look at *Epydoc*, which also understands reST."
    (http://sphinx-doc.org/intro.html#prerequisites)

Premiers pas
------------

Générer la doc::

    mkdir docs
    sphinx-quickstart

Autodoc
-------

- http://sphinx-doc.org/tutorial.html#autodoc
- http://sphinx-doc.org/ext/autodoc.html

Lorsqu'on utilise::

    .. automodule:: foo.bar
        :members:

seuls les membres définis dans __all__ sont importés.

Les docstring des constructeurs de classes __init__() sont ignorés par défaut.
En fait, il n'est pas nécessaire/recommandé de mettre une docstring aux
constructeur (pylint ne râle pas), la description des arguments du constructeur
doit à priori être faite dans la docstring de la classe.

On peut néanmoins obliger sphinx à générer la documentation des constructeurs:
http://stackoverflow.com/questions/5599254/how-to-use-sphinxs-autodoc-to-document-a-classs-init-self-method


Les PEPs ne définissent pas vraiment le contenu des docstring, seulement le
langage de markup et l'intégration des docstrings dans le code.
Autrement dit, il n'y a pas de notation standard pour decrire les parametre, la
valeur de retour, etc (contrairement à javadoc par exemple).

Le mieux est alors de s'inspirer de ce qui ce fait de mieux...

Styles de docstring:
- Pillow (ex: https://github.com/python-pillow/Pillow/blob/master/PIL/Image.py) et PIP (https://github.com/pypa/pip/blob/develop/pip/index.py), simple et élégant::

    def getmodebandnames(mode):
        """
        Gets a list of individual band names.  Given a mode, this function returns
        a tuple containing the names of individual bands (use
        :py:method:`~PIL.Image.getmodetype` to get the mode used to store each
        individual band.

        :param mode: Input mode.
        :returns: A tuple containing band names.  The length of the tuple
            gives the number of bands in an image of the given mode.
        :exception KeyError: If the input mode was not a standard mode.
        """
        return ImageMode.getmode(mode).bands


- Matplotlib (ex: https://github.com/matplotlib/matplotlib/blob/master/lib/matplotlib/animation.py)::

    def __init__(self, fps=5, codec=None, bitrate=None, extra_args=None, metadata=None):
        '''
        Construct a new MovieWriter object.

        fps: int
            Framerate for movie.
        codec: string or None, optional
            The codec to use. If None (the default) the setting in the
            rcParam `animation.codec` is used.
        bitrate: int or None, optional
            The bitrate for the saved movie file, which is one way to control
            the output file size and quality. The default value is None,
            which uses the value stored in the rcParam `animation.bitrate`.
            A value of -1 implies that the bitrate should be determined
            automatically by the underlying utility.
        extra_args: list of strings or None
            A list of extra string arguments to be passed to the underlying
            movie utiltiy. The default is None, which passes the additional
            argurments in the 'animation.extra_args' rcParam.
        metadata: dict of string:string or None
            A dictionary of keys and values for metadata to include in the
            output file. Some keys that may be of use include:
            title, artist, genre, subject, copyright, srcform, comment.
        '''

- Mayavi (ex: https://github.com/enthought/mayavi/blob/master/mayavi/core/engine.py)::

    def add_scene(self, scene, name=None):
        """Add given `scene` (a `pyface.tvtk.scene.Scene` instance) to
        the mayavi engine so that mayavi can manage the scene.  This
        is used when the user creates a scene.  Note that for the
        `EnvisageEngine` this is automatically taken care of when you
        create a new scene using the TVTK scene plugin.

        Parameters:
        -----------

         scene - `pyface.tvtk.scene.Scene`

          The scene that needs to be managed from mayavi.

         name - `str`

          The name assigned to the scene.  It tries to determine the
          name of the scene from the passed scene instance.  If this
          is not possible it defaults to 'Mayavi Scene'.
        """

- Scipy (ex: https://github.com/scipy/scipy/blob/master/scipy/linalg/decomp_cholesky.py)::

    def cholesky(a, lower=False, overwrite_a=False, check_finite=True):
        """
        Compute the Cholesky decomposition of a matrix.

        Returns the Cholesky decomposition, :math:`A = L L^*` or
        :math:`A = U^* U` of a Hermitian positive-definite matrix A.

        Parameters
        ----------
        a : (M, M) array_like
            Matrix to be decomposed
        lower : bool, optional
            Whether to compute the upper or lower triangular Cholesky
            factorization.  Default is upper-triangular.
        overwrite_a : bool, optional
            Whether to overwrite data in `a` (may improve performance).
        check_finite : bool, optional
            Whether to check that the input matrix contains only finite numbers.
            Disabling may give a performance gain, but may result in problems
            (crashes, non-termination) if the inputs do contain infinities or NaNs.

        Returns
        -------
        c : (M, M) ndarray
            Upper- or lower-triangular Cholesky factor of `a`.

        Raises
        ------
        LinAlgError : if decomposition fails.

        Examples
        --------
        >>> from scipy import array, linalg, dot
        >>> a = array([[1,-2j],[2j,5]])
        >>> L = linalg.cholesky(a, lower=True)
        >>> L
        array([[ 1.+0.j,  0.+0.j],
               [ 0.+2.j,  1.+0.j]])
        >>> dot(L, L.T.conj())
        array([[ 1.+0.j,  0.-2.j],
               [ 0.+2.j,  5.+0.j]])

        """

- http://sphinxcontrib-napoleon.readthedocs.org/en/latest/example_numpy.html::

    def module_level_function(param1, param2=None, *args, **kwargs):
    """This is an example of a module level function.

    Function parameters should be documented in the ``Parameters`` section.
    The name of each parameter is required. The type and description of each
    parameter is optional, but should be included if not obvious.

    Parameter types -- if given -- should be specified according to
    `PEP 484`_, though `PEP 484`_ conformance isn't required or enforced.

    If \*args or \*\*kwargs are accepted,
    they should be listed as ``*args`` and ``**kwargs``.

    The format for a parameter is::

        name : type
            description

            The description may span multiple lines. Following lines
            should be indented to match the first line of the description.
            The ": type" is optional.

            Multiple paragraphs are supported in parameter
            descriptions.

    Parameters
    ----------
    param1 : int
        The first parameter.
    param2 : Optional[str]
        The second parameter.
    *args
        Variable length argument list.
    **kwargs
        Arbitrary keyword arguments.

    Returns
    -------
    bool
        True if successful, False otherwise.

        The return type is not optional. The ``Returns`` section may span
        multiple lines and paragraphs. Following lines should be indented to
        match the first line of the description.

        The ``Returns`` section supports any reStructuredText formatting,
        including literal blocks::

            {
                'param1': param1,
                'param2': param2
            }

    Raises
    ------
    AttributeError
        The ``Raises`` section is a list of all exceptions
        that are relevant to the interface.
    ValueError
        If `param2` is equal to `param1`.


    .. _PEP 484:
       https://www.python.org/dev/peps/pep-0484/

    """
    if param1 == param2:
        raise ValueError('param1 may not be equal to param2')
    return True

- Numpy (ex: https://github.com/numpy/numpy/blob/master/numpy/core/numeric.py)::

    def full_like(a, fill_value, dtype=None, order='K', subok=True):
        """
        Return a full array with the same shape and type as a given array.

        Parameters
        ----------
        a : array_like
            The shape and data-type of `a` define these same attributes of
            the returned array.
        fill_value : scalar
            Fill value.
        dtype : data-type, optional
            Overrides the data type of the result.
        order : {'C', 'F', 'A', or 'K'}, optional
            Overrides the memory layout of the result. 'C' means C-order,
            'F' means F-order, 'A' means 'F' if `a` is Fortran contiguous,
            'C' otherwise. 'K' means match the layout of `a` as closely
            as possible.
        subok : bool, optional.
            If True, then the newly created array will use the sub-class
            type of 'a', otherwise it will be a base-class array. Defaults
            to True.

        Returns
        -------
        out : ndarray
            Array of `fill_value` with the same shape and type as `a`.

        See Also
        --------
        zeros_like : Return an array of zeros with shape and type of input.
        ones_like : Return an array of ones with shape and type of input.
        empty_like : Return an empty array with shape and type of input.
        zeros : Return a new array setting values to zero.
        ones : Return a new array setting values to one.
        empty : Return a new uninitialized array.
        full : Fill a new array.

        Examples
        --------
        >>> x = np.arange(6, dtype=np.int)
        >>> np.full_like(x, 1)
        array([1, 1, 1, 1, 1, 1])
        >>> np.full_like(x, 0.1)
        array([0, 0, 0, 0, 0, 0])
        >>> np.full_like(x, 0.1, dtype=np.double)
        array([ 0.1,  0.1,  0.1,  0.1,  0.1,  0.1])
        >>> np.full_like(x, np.nan, dtype=np.double)
        array([ nan,  nan,  nan,  nan,  nan,  nan])

        >>> y = np.arange(6, dtype=np.double)
        >>> np.full_like(y, 0.1)
        array([ 0.1,  0.1,  0.1,  0.1,  0.1,  0.1])

        """
        res = empty_like(a, dtype=dtype, order=order, subok=subok)
        multiarray.copyto(res, fill_value, casting='unsafe')
        return res


Il semble y avoir 2 principaux styles éprouvés:

- la première méthode (Pillow, PIP) semble être le sytle officiel recommandé par sphinx:

  - cf. http://stackoverflow.com/questions/5334531/python-documentation-standard-for-docstring
  - cf. http://sphinx-doc.org/domains.html#info-field-lists

- un style alternatif semble rencontrer un certain succès aussi: celui de Numpy
  et Google (cf. section "Napoleon" ci-dessous).


Napoleon is a Sphinx extension
------------------------------

Numpy et Google utilisent un style éprouvé différent de celui recommandé par sphinx:

- http://sphinxcontrib-napoleon.readthedocs.org/
- http://sphinx-doc.org/ext/napoleon.html#module-sphinx.ext.napoleon
- http://sphinxcontrib-napoleon.readthedocs.org/en/latest/example_numpy.html
- http://sphinxcontrib-napoleon.readthedocs.org/en/latest/example_google.html#example-google

    Napoleon is a Sphinx extension that enables Sphinx to parse both NumPy and
    Google style docstrings - the style recommended by Khan Academy.

    Napoleon is a pre-processor that parses NumPy and Google style docstrings
    and converts them to reStructuredText before Sphinx attempts to parse them.
    This happens in an intermediate step while Sphinx is processing the
    documentation, so it doesn’t modify any of the docstrings in your actual source
    code files.
    (http://sphinxcontrib-napoleon.readthedocs.org)

Odt2sphinx
----------

https://pypi.python.org/pypi/odt2sphinx/ (http://sphinx-doc.org/intro.html#conversion-from-other-systems)

Themes
------

http://docs.writethedocs.org/tools/sphinx-themes/

Builtin themes (cf. http://sphinx-doc.org/theming.html):

- basic
- alabaster
- sphinx_rtd_theme
- classic
- sphinxdoc
- scrolls
- agogo
- nature
- pyramid
- haiku
- traditional
- epub
- bizstyle

3 themes semblent avoir la cote:

- Read the Docs Theme https://github.com/snide/sphinx_rtd_theme
- Alabaster https://github.com/bitprophet/alabaster
- Sphinx Bootstrap Theme https://github.com/ryan-roemer/sphinx-bootstrap-theme

Thèmes disponibles sur Debian 8 (nom des paquets):

- python3-sphinx-rtd-theme
- python-guzzle-sphinx-theme
- doctrine-sphinx-theme
- python-oslosphinx

Extensions disponibles sur Debian 8
-----------------------------------

Nom des paquets:

- python3-sphinxcontrib.actdiag
- python3-sphinxcontrib.blockdiag
- python3-sphinxcontrib.nwdiag
- python3-sphinxcontrib.programoutput
- python3-sphinxcontrib.seqdiag
- python3-sphinxcontrib.youtube

