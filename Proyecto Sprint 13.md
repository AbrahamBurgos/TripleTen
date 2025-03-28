# Proyecto Final

# Telecomunicaciones: identificar operadores ineficaces

# Objetivo:

Desarrollar e implementar una nueva funcionalidad en la plataforma de telefonía virtual CallMeMaybe que permita a los supervisores identificar a los operadores con menor desempeño. Para ello, se analizarán métricas clave como la cantidad de llamadas entrantes perdidas (internas y externas), los tiempos de espera prolongados y, en el caso de operadores responsables de realizar llamadas salientes, un bajo volumen de estas. El objetivo es proporcionar información clara y accionable que contribuya a mejorar la eficiencia operativa y la calidad del servicio.

Indice:

1. Análisis exploratorio de datos
2. Identificion de operadores ineficaces
3. Pruebas de hipótesis estadísticas


```python
import pandas as pd

# Cargar los datasets
telecom_data = pd.read_csv("telecom_dataset_us.csv")
clients_data = pd.read_csv("telecom_clients_us.csv")

# Mostrar las primeras filas de cada dataset
telecom_head = telecom_data.head()
clients_head = clients_data.head()

# Verificar valores nulos en ambos datasets
telecom_nulls = telecom_data.isnull().sum()
clients_nulls = clients_data.isnull().sum()

# Mostrar información general de los datasets
telecom_info = telecom_data.info()
clients_info = clients_data.info()

telecom_head, clients_head, telecom_nulls, clients_nulls

```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    Cell In[5], line 4
          1 import pandas as pd
          3 # Cargar los datasets
    ----> 4 telecom_data = pd.read_csv("telecom_dataset_us.csv")
          5 clients_data = pd.read_csv("telecom_clients_us.csv")
          7 # Mostrar las primeras filas de cada dataset


    File /opt/conda/envs/python3/lib/python3.9/site-packages/pandas/io/parsers.py:610, in read_csv(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, squeeze, prefix, mangle_dupe_cols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, dialect, error_bad_lines, warn_bad_lines, delim_whitespace, low_memory, memory_map, float_precision, storage_options)
        605 kwds_defaults = _refine_defaults_read(
        606     dialect, delimiter, delim_whitespace, engine, sep, defaults={"delimiter": ","}
        607 )
        608 kwds.update(kwds_defaults)
    --> 610 return _read(filepath_or_buffer, kwds)


    File /opt/conda/envs/python3/lib/python3.9/site-packages/pandas/io/parsers.py:462, in _read(filepath_or_buffer, kwds)
        459 _validate_names(kwds.get("names", None))
        461 # Create the parser.
    --> 462 parser = TextFileReader(filepath_or_buffer, **kwds)
        464 if chunksize or iterator:
        465     return parser


    File /opt/conda/envs/python3/lib/python3.9/site-packages/pandas/io/parsers.py:819, in TextFileReader.__init__(self, f, engine, **kwds)
        816 if "has_index_names" in kwds:
        817     self.options["has_index_names"] = kwds["has_index_names"]
    --> 819 self._engine = self._make_engine(self.engine)


    File /opt/conda/envs/python3/lib/python3.9/site-packages/pandas/io/parsers.py:1050, in TextFileReader._make_engine(self, engine)
       1046     raise ValueError(
       1047         f"Unknown engine: {engine} (valid options are {mapping.keys()})"
       1048     )
       1049 # error: Too many arguments for "ParserBase"
    -> 1050 return mapping[engine](self.f, **self.options)


    File /opt/conda/envs/python3/lib/python3.9/site-packages/pandas/io/parsers.py:1867, in CParserWrapper.__init__(self, src, **kwds)
       1864 kwds["usecols"] = self.usecols
       1866 # open handles
    -> 1867 self._open_handles(src, kwds)
       1868 assert self.handles is not None
       1869 for key in ("storage_options", "encoding", "memory_map", "compression"):


    File /opt/conda/envs/python3/lib/python3.9/site-packages/pandas/io/parsers.py:1362, in ParserBase._open_handles(self, src, kwds)
       1358 def _open_handles(self, src: FilePathOrBuffer, kwds: Dict[str, Any]) -> None:
       1359     """
       1360     Let the readers open IOHanldes after they are done with their potential raises.
       1361     """
    -> 1362     self.handles = get_handle(
       1363         src,
       1364         "r",
       1365         encoding=kwds.get("encoding", None),
       1366         compression=kwds.get("compression", None),
       1367         memory_map=kwds.get("memory_map", False),
       1368         storage_options=kwds.get("storage_options", None),
       1369     )


    File /opt/conda/envs/python3/lib/python3.9/site-packages/pandas/io/common.py:642, in get_handle(path_or_buf, mode, encoding, compression, memory_map, is_text, errors, storage_options)
        640         errors = "replace"
        641     # Encoding
    --> 642     handle = open(
        643         handle,
        644         ioargs.mode,
        645         encoding=ioargs.encoding,
        646         errors=errors,
        647         newline="",
        648     )
        649 else:
        650     # Binary mode
        651     handle = open(handle, ioargs.mode)


    FileNotFoundError: [Errno 2] No such file or directory: 'telecom_dataset_us.csv'



```python

```
