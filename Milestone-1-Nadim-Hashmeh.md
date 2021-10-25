# Project write-up for Milestone 1 - Nadim Hashmeh, CMPS 6160

Background: Mars has two polar caps that are largely composed of water ice, like Earth. Planetary scientists measure the amount of electromagnetic radiation reflected off the polar cap surface as well as dielectric interfaces in the subsurface using active radar sounding to learn more about its composition and internal structure. The strength of radar reflections is mostly determined by the contrast in dielectric properties between two overlying materials, such as the atmosphere and ice, or ice and rock. Radar reflections at the surface and below are typically represented as bright "reflectors" in cross-sectional images known as radargrams. The data that comprises these radargrams are three dimensional: horizontal position, vertical position, and brightness (relative power of reflection). Using these, scientists can analyze the vertical distribution of dielectric contrasts that are sensitive to the frequency of the radar being used.

Motivation: For my PhD, I am attempting to explain the unexpected behavior of high frequency radar at the south polar cap in order to gain more understanding about its interior structure, distribution of material, and surface texture. High frequency radar behavior (20 MHz) at the south polar cap differs from its northern counterpart, as well as many typical glacier observations on Earth, in that it is often incoherent and rapidly attenuates before reaching the basal interface, if it even reaches the base at all. At lower frequencies (~5 MHz), this behavior is not observed in either polar cap. Therefore, some property of the south polar cap is sensitive to scattering radar at relatively higher frequencies. One way to investigate this is to compare the basal reflector power to the thickness of material above it. One would expect a negative correlation between these two variables, and in my own work, I have observed it in some areas. However, there are many unexpected instances where it does not follow the same trend. My broader research goals aim to explain this behavior, and one avenue I have considered is looking at the role of surface slope in influencing the propagation of radar through the south polar ice.

Data: I have surface and basal reflector information for both south and north polar caps. SHAllow RADar (SHARAD) radargrams are available in NASA's Planetary Data System archive, which I used to extract the reflector position and power information from using a variety of tools during my own research. This compiled dataset contains the orbit number, reflector identifier, vertical pixel position, surface elevation, raw radar power, latitude, longitude, and spatial categorical information of pairs of surface and basal reflectors. 

Plan and question(s) to be answered: I will use Python to calculate the slope of each surface reflector I have mapped and compare that information to ice thickness and reflector power values to see if surface slope shows any correlation across these variables. Basically, do steeper surfaces affect the detection of the base in any notable way? I will also explore relationships between these values and the spatial categorical data they contain to note the regional distribution of my observations.

### Project website: 
https://github.com/nhashmeh/nhashmeh.github.io

### Project data: 
https://github.com/nhashmeh/nhashmeh.github.io/tree/main/data

#### Raw SHARAD data: 
https://pds-geosciences.wustl.edu/missions/mro/sharad.htm

#### SHARAD instrument documentation: 
Seu, R., Phillips, R. J., Biccari, D., Orosei, R., Masdea, A., Picardi, G., Safaeinili, A., Campbell, B. A., Plaut, J. J., Marinangeli, L., Smrekar, S. E., & Nunes, D. C. (2007). SHARAD sounding radar on the Mars Reconnaissance Orbiter. Journal of Geophysical Research, 112(E5), E05S05. https://doi.org/10.1029/2006JE002745



```python
# relevant libraries
import pandas as pd
import os
```


```python
os.getcwd()
```




    '/Users/nadim/Documents/datascience_finalproject/nhashmeh.github.io/notebooks'




```python
# import data

all_data = pd.read_csv('nhashmeh.github.io/data/spld_data_6160project.csv',header=0)
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    <ipython-input-6-0df5f8e759c4> in <module>
          1 # import data
          2 
    ----> 3 all_data = pd.read_csv('nhashmeh.github.io/data/spld_data_6160project.csv',header=0)
    

    ~/opt/anaconda3/lib/python3.8/site-packages/pandas/io/parsers.py in read_csv(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, squeeze, prefix, mangle_dupe_cols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, dialect, error_bad_lines, warn_bad_lines, delim_whitespace, low_memory, memory_map, float_precision, storage_options)
        608     kwds.update(kwds_defaults)
        609 
    --> 610     return _read(filepath_or_buffer, kwds)
        611 
        612 


    ~/opt/anaconda3/lib/python3.8/site-packages/pandas/io/parsers.py in _read(filepath_or_buffer, kwds)
        460 
        461     # Create the parser.
    --> 462     parser = TextFileReader(filepath_or_buffer, **kwds)
        463 
        464     if chunksize or iterator:


    ~/opt/anaconda3/lib/python3.8/site-packages/pandas/io/parsers.py in __init__(self, f, engine, **kwds)
        817             self.options["has_index_names"] = kwds["has_index_names"]
        818 
    --> 819         self._engine = self._make_engine(self.engine)
        820 
        821     def close(self):


    ~/opt/anaconda3/lib/python3.8/site-packages/pandas/io/parsers.py in _make_engine(self, engine)
       1048             )
       1049         # error: Too many arguments for "ParserBase"
    -> 1050         return mapping[engine](self.f, **self.options)  # type: ignore[call-arg]
       1051 
       1052     def _failover_to_python(self):


    ~/opt/anaconda3/lib/python3.8/site-packages/pandas/io/parsers.py in __init__(self, src, **kwds)
       1865 
       1866         # open handles
    -> 1867         self._open_handles(src, kwds)
       1868         assert self.handles is not None
       1869         for key in ("storage_options", "encoding", "memory_map", "compression"):


    ~/opt/anaconda3/lib/python3.8/site-packages/pandas/io/parsers.py in _open_handles(self, src, kwds)
       1360         Let the readers open IOHanldes after they are done with their potential raises.
       1361         """
    -> 1362         self.handles = get_handle(
       1363             src,
       1364             "r",


    ~/opt/anaconda3/lib/python3.8/site-packages/pandas/io/common.py in get_handle(path_or_buf, mode, encoding, compression, memory_map, is_text, errors, storage_options)
        640                 errors = "replace"
        641             # Encoding
    --> 642             handle = open(
        643                 handle,
        644                 ioargs.mode,


    FileNotFoundError: [Errno 2] No such file or directory: 'nhashmeh.github.io/data/spld_data_6160project.csv'



```python

```
