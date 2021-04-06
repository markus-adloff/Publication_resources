################################################################
### readme.txt #################################################
################################################################

For:
'Inclusion of a suite of weathering tracers in the cGENIE Earth System Model - muffin release v.0.9.22'
Markus Adloff, Andy Ridgwell, Fanny M. Monteiro, Ian J. Parkinson, Alexander Dickson, PhilipA. E. Pogge von Strandmann, Matthew Fantle, and Sarah E. Greene

################################################################
10/07/2020 -- README.txt file creation (M.A.)
30/03/2021 -- Added details for sensitivity studies (M.A.)
################################################################

Provided is the code used to create the model experiments presented in the paper.
Also given are the configuration files necessary to run these experiments.

The intention is to provide an oppertunity to question the assumptions and
interpretation through re-analysis and the creation of new and different experiments.
(Plus, to provide a means to replicate results.)

### code version and installation ##############################

Instructions for installing the model code, 
as well as a series of tutorials for learning how to configure, run, and analyses the model output, can be  found here:

http://www.seao2.info/mycgenie.html

See 'got muffin?' quick start guides for installing the code.

Refer to the cGENIE.muffin combined user-manual and an introduction to Earth system modelling tutorials for a complete set of model documentation:

http://www.seao2.info/cgenie/docs/muffin.pdf

### addition of configuration and forcing files ################

Add the provided base-configuration file cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2_OsSrLiCa.BASE to $HOME/cgenie.muffin/genie-main/configs/
Add the provided user-configuration files to $HOME/cgenie.muffin/genie-userconfigs
Add the provided forcing folder worbe2.FpCO2_Fp13CO2.detplusopalSED_year2 to $HOME/cgenie.muffin/genie-forcings

### addition of an updated reef mask for the present-day #######

An updated reef mask for the present-day ocean is provided, based on ETOPO5 bathymetry dataset. A detailed description and test configurations are described in GRID.txt.

To run the spin-ups and simulations presented in Adloff et al. 2020, add the provided reef mask worbe2.190813.reefmask.36x36, worbe2.190813.depth.36x36 and worbe2.190813.sedcoremask.36x36 to $HOME/cgenie.muffin/genie-sedgem/data/input/

### model experiments -- spinups ###############################

All experiments are run from:
$HOME/cgenie.muffin/genie-main
(unless a different installation directory has been used)
In the given command lines, it is assumed that the user-configuration files are in $HOME/cgenie.muffin/genie-userconfigs. If they are in a different location, please replace '/' in the command line by the relative path from $HOME/cgenie.muffin/genie-userconfigs to the location of the user-configuration files.

The commands to run the spinups are listed as follows:

(1a) INITIAL SPINUP

The initial, 1st-stage closed system spin-up as detailed in the Methods section of the paper:

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2 / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN1 20000

(1b) Second Stage SPINUP

The follow-on, 2nd-stage open system and accelerated spin-up:

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2 / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN2gl_noRCO2 500000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN1

(1c) Third Stage SPINUPs

The follow-on, 3rd-stage open system and accelerated spin-ups with metal isotopes:

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2_OsSrLiCa / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_FLUXES 15000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN2gl_noRCO2

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2_OsSrLiCa / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_TUNED 15000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN2gl_noRCO2

### model experiments -- pulsed C injection ####################

For transient simulations of the response to a sudden C injection:

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2_OsSrLiCa / Transient_1000PgC 15000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_FLUXES

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2_OsSrLiCa / Transient_5000PgC 15000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_FLUXES

### model experiments -- sensitivity studies ###################

We ran the following sensitivity experiments for indivitual metal cycles:

(2a) Osmium -- 2D weathering

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2 / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN2gl_GEMCO2 500000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN1

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2 / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_GEMCO2 5000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN2gl_GEMCO2

(2b) Osmium -- watercolumn scavenging

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2 / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_Osscav 5000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN2gl_noRCO2

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2_OsSrLiCa / Transient_1000PgC_Osscav 200000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_Osscav

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2_OsSrLiCa / Transient_5000PgC_Osscav 200000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_Osscav

(2c) Lithium -- climate effect on terrestrial clay formation

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2 / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_WDLi 5000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN2gl_noRCO2

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2_OsSrLiCa / Transient_1000PgC_WDLi 10000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_WDLi

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2_OsSrLiCa / Transient_5000PgC_WDLi 10000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_WDLi

(2d) Calcium -- different fractionation schemes for biogenic carbonate production

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2 / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_CaA 20000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN2gl_noRCO2

./runmuffin.sh cgenie.eb_go_gs_ac_bg_sg_rg_gl.worbe2 / spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN3gl_CaB 20000000 spinup.worbe2.RidgwellHargreaves1997_S36x36.SPIN2gl_noRCO2


Please contact the authors for questions about the model parameter file configurations.

################################################################
################################################################
################################################################
