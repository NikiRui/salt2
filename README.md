## SALT2 PYTHON MODULE ##

Python module interface to the SALT2 supernova lightcurve templates

Stephen Bailey
Summer 2012

## OVERVIEW ##

This code provides a python interface to the salt2 supernovae timeseries
model.  Note that this does not run salt2 or directly perform SN lightcurve
or spectra fits.  It is primarily intended as an interface/interpolator
of the salt2 model.

The Salt2Model class does provide a few experimental methods such as
chi2spectrum(), chi2spectra(), and fitspectra() intended for fitting
the salt2 model to a set of observed spectra.  In practice, I found the
accuracy of the fit was driven by the salt2 error model and further work
would be needed to make that more accurate in order to make these fits
quantitatively useful.

## INSTALLATION ##

Add the salt2/python/ directory to your PYTHONPATH, or otherwise move
salt2/python/salt2.py into another directory which is in your PYTHONPATH.
If someone wants to contribute a disutils setup.py, that would be welcome.

## USAGE ##

Create a Salt2Model model object, using whatever the latest salt2* model
files are available in $PYTHONPATH:

    m = salt2.model()
    
Use a specific salt2 model directory:

    m = salt2.model('/data/salt2models/salt2-2-2')
    
Find the wavelengths at which the model is natively sampled:

    w = m.wavelengths()
    
Find the model flux at at phase=0 for defaults x1=0.0 c=0.0:

    flux = m.flux(0)

find the model flux at an arbitrary phase, x1, and c:

    flux = m.flux(phase=10.3, x1=0.5, c=0.2)
    
Evaluate the model on a different wavelength grid:

    w = N.arange(2000.0, 8001.0, 5.0)
    flux = m.flux(phase=0, x1=0.5, c=0.2, wavelengths=w)
    
Get the model error or variance=error**2:

    err = m.error(phase=0.0)
    var = m.variance(phase=0.0, x1=0.5)
    
## SALT2 MODEL FILES ##

For convenience, this package comes bundled with salt2 model templates
originally available from Julien Guy at:

    http://supernovae.in2p3.fr/~guy/salt/download_templates.html
    
A more recent version of the templates may be available at that site.
These templates are included here with Julien's permission.

