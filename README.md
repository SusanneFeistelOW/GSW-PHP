GSW-PHP
=======

PHP implementation of the Thermodynamic Equation Of Seawater - 2010 (TEOS-10)


TEOS-10 v3.03 GSW Oceanographic Toolbox in PHP

This is a translation of the C code into PHP (version 5.3.8).
You should download the documentation from http://teos-10.org.

The functions gsw_saar and gsw_delta_sa_ref
have been modified from the original to not use an external
data file for global absolute salinity anomaly and absolute
salinity anomaly ratio data. The data are instead incorporated
into static tables that are used directly.

Files:
******
readme.txt
                        - this file.
TEOS10_GSW.php
                        - PHP implementation of the check functions

TEOS10_gsw_oceanographic_toolbox.php
                        - The PHP GSW library (v3.03) less gsw_saar

TEOS10_gsw_oceanographic_toolbox_v304.php
                        - partial translation of v3.04 Matlab version

TEOS10_gsw_saar.php
                        - gsw_saar and gsw_deltasa_atlas (modified)

TEOS10_gsw_saar_data.inc.php
                        - static global absolute salinity anomaly data
                          used by gsw_saar.c and created by gsw_format

Gibbs SeaWater (GSW) Oceanographic Toolbox of TEOS-10 version 3.pdf
                        - pdf printout of the check values


Installation:
*************
Copy all php files in a directory on your web server.
Call http://your.webserver.com/your-directory/TEOS10_GSW.php
to see functions and check values.

To use the GSW library (v3.03) in your php code,
include_once the following files:
    "TEOS10_gsw_oceanographic_toolbox.php";
    "TEOS10_gsw_saar.php";

You can then load the libraries
    $TEOS10 = new TEOS10_gsw_oceanographic_toolbox();
    $GSW_saar = new TEOS10_gsw_saar();

To use the already translated methods from v3.04
include_once the following file:
    "TEOS10_gsw_oceanographic_toolbox_v304.php";
and overwrite the original 3.03 library
with the extended version
    $TEOS10 = new TEOS10_gsw_oceanographic_toolbox_v304();

NOTE:   The partial v3.04 toolbox is not a stand-alone version!
        It needs all other files to work.

Call the gsw functions as methods like this:
    $TEOS10->gsw_sa_from_sp($sp,$p,$lon,$lat);

The PHP code was created using an Apache 2.2 server and PHP version 5.3.8

ChangeLog:
**********
2013-05-30:     gsw-3.03
                added functions:
                    ! gsw_sp_from_c           - Practical Salinity from conductivity - Converted from fortran by Bernard Saulmé
                    ! gsw_c_from_sp           - conductivity from Practical Salinity - Converted from fortran by Bernard Saulmé
                    ! gsw_sp_from_sk          - Practical Salinity from Knudsen Salinity
                    ! gsw_z_from_p            - height from pressure
                    ! gsw_adiabatic_lapse_rate_from_ct - adiabatic lapse rate from CT
                    ! gsw_alpha_on_beta       - alpha divided by beta
                    ! gsw_rho_first_derivatives  - first derivatives of density - Converted from Matlab by Bernard Saulmé, adapted from C by Susanne Feistel
                    ! gsw_sigma0              - sigma0 with reference pressure of 0 dbar
                    ! gsw_sigma1              - sigma1 with reference pressure of 1000 dbar
                    ! gsw_sigma2              - sigma2 with reference pressure of 2000 dbar
                    ! gsw_sigma3              - sigma3 with reference pressure of 3000 dbar
                    ! gsw_sigma4              - sigma4 with reference pressure of 4000 dbar
                    ! gsw_kappa               - isentropic compressibility
                    ! gsw_cabbeling           - cabbeling coefficient
                    ! gsw_thermobaric         - thermobaric coefficient
                    ! gsw_sa_from_rho         - Absolute salinity from rho, ct and p - Converted from fortran by Bernard Saulmé
                    ! gsw_nsquared            - buoyancy (Brunt-Vaisala) frequency squared (N^2)
                    ! gsw_turner_rsubrho      - Turner angle & Rsubrho
                    ! gsw_ipv_vs_fnsquared_ratio  - ratio of the vertical gradient of potential density
                    ! gsw_grav                - gravitational acceleration
                    ! gsw_enthalpy_sso_0_p    - enthalpy at (SSO,CT=0,p)

                renamed functions:
                    ! gsw_delta_sa_ref to gsw_deltasa_atlas
                    ! gsw_entropy_t_exact to gsw_entropy_from_t

                misc:
                    - Bug fix in TEOS10_GSW.php
                    - moved constant values from class properties to methods

2013-07-08:        gsw-3.0 Initial creation.

Translations
************
From C:
Susanne Feistel <susanne.feistel@io-warnemuende.de>
Leibniz-Institut für Ostseeforschung Warnemünde
Seestrasse 15
18119 Rostock
Germany

From Matlab, Fortran:
Bernard Saulmé 17/09/2013
Contact: b92@wanadoo.fr
