GraFFT
======

Frequency-domain analysis for Graphite data written in Python 3.
----------------------------------------------------------------

Graphite (and its Carbon database) assume time-series data. Sometimes it's useful to see if there is any frequency component to a set of metrics. For instance, CPU load might be spiking once per minute, suggesting a regular, frequent pattern to the metrics.

GraFFT is designed to take Graphite data via the Graphite REST API, and run this data through a Discrete Fourier Transform - using the Fast Fourier Transform (FFT) algorithm - in order to identify any frequencies in the data.

GraFFT currently uses the Numpy FFT routines, although support for pyFFTW might be added later. 

The data pipeline looks something like this:

```
Setup query (GraFFT) 
Return JSON (Graphite API)
Parse JSON (GraFFT)
Calculate FFT and return results (Numpy)
Convert to JSON and output (GraFFT)
```

This allows GraFFT to present frequency-domain results to any application which can display them, such as a charting library or monitoring tool.

Notes
-----
Because the DFT assumes that samples are taken at regular time intervals, GraFFT works best with Graphite data which has been sampled every N seconds/minutes/etc. Data in Graphite which derives from irregular events (such as transactions) is not suitable for GraFFT.

Dependencies
------------
* Python 3.2
* NumPy 3.2
