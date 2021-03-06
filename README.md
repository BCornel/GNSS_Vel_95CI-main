# GNSS_Vel_95CI
A Python program for calculating the 95%CI for GNSS-derived site velocities, by B. Cornelison and G. Wang. GNSS_Vel_95CI calculates the site velocity and the 95%CI for a given GNSS-derived daily displacement time series using methods outlined in Wang (2022). The plots and text files containing the calculated results can be controlled in the function calls.

## Important Links
GitHub repositories: [GitHub1](https://github.com/bob-Github-2020), [Github2](https://github.com/BCornel)

Pypi package index: [pip](https://pypi.org/project/GNSS-VEL-95CI/)

This module can be called as:
```python
from GNSS_Vel_95CI import cal_95CI
```

## Installation and Dependencies
You may need to install "statsmodels" on your computer if you have not used it before, which is the only dependency used that is not in the standard Python library.

Install statsmodel example:
```bash
pip install statsmodels
```
Use the package manager [pip](https://pypi.org/project/GNSS-VEL-95CI/) to install GNSS_VEL_95CI
```bash
pip install GNSS_Vel_95CI
```
To uninstall GNSS_Vel_95CI:
```bash
pip uninstall GNSS_Vel_95CI
```

To show current version of GNSS_Vel_95CI:
```bash
python -m pip show GNSS_Vel_95CI
```
In order to upgrade versions, use the following command:
```bash
python -m pip install -U GNSS_Vel_CI95
```
## Basic usage
### GNSS file example
```
Decimal-Year  NS(cm)  EW(cm)  UD(cm)
An example of 'fin': UH01_GOM20_neu_cm.col
Decimal-Year      NS(cm)       EW(cm)       UD(cm)  sigma-NS(cm)  sigma-EW(cm)  sigma-UD(cm)
2012.7447       0.0501       0.1444       0.3072       0.0495       0.0217       0.0541
2012.7474       0.0336      -0.1013      -0.3132       0.0485       0.0208       0.0527
2012.7502      -0.1226       0.0234       0.3309       0.0499       0.0215       0.0544
2012.7529      -0.0505      -0.0609      -0.4559       0.0487       0.0217       0.0534
```
### Basic script example
```python
import os
import pandas as pd
from GNSS_Vel_95CI import cal_95CI

# loop through EW, NS and UD columns
directory = './'   # for unix directory (for windows use windows directory)
for fin in os.listdir(directory):
   if fin.endswith("neu_cm.col"):
      print(fin)
      GNSS = fin[0:4]    # station name, e.g., UH01
      ts_enu = []
      ts_enu = pd.read_csv (fin, header=0, delim_whitespace=True)
      year = ts_enu.iloc[:,0]    # decimal year

      dis = ts_enu.iloc[:,1]     # NS
      result_NS=cal_95CI(year,dis,GNSS,DIR='NS',output='on', pltshow='on')
      b_NS=round(result_NS[0],2)          # slope, or site velocity
      b_NS_95CI=round(result_NS[1],2)      # The 95%CI of slope

      dis = ts_enu.iloc[:,2]     # EW
      result_EW=cal_95CI(year,dis,GNSS,DIR='EW',output='on',pltshow='on')
      b_EW=round(result_EW[0],2)
      b_EW_95CI=round(result_EW[1],2)
    
      dis = ts_enu.iloc[:,3]     # UD
      result_UD=cal_95CI(year,dis,GNSS,DIR='UD',output='on',pltshow='on')
      b_UD=round(result_UD[0],2)
      b_UD_95CI=round(result_UD[1],2)
   
   else:
      continue
```
## Example Figures
![MRHK_UD_ACF](https://user-images.githubusercontent.com/65426380/144933002-c7eeab12-a110-4031-93b2-120011c5340f.png)

![MRHK_UD_Decomposition](https://user-images.githubusercontent.com/65426380/144967345-ca5b2264-c82e-46cf-8eed-a23d8466f6f9.png)
## Detailed Method
[Methods_Vel_95CI.pdf](https://github.com/bob-Github-2020/GNSS_Vel_95CI/files/7664316/Methods_Vel_95CI.pdf)
## Contributing
Pull requests are welcome and comments. For major changes, please open an issue first to discuss what you would like to change.
Please make sure to update tests as appropriate and contact: bscornelison@gmail.com or bob.g.wang@gmail.com
## Citation
If you use GNSS_Vel_95CI in a scientific publication, we would appreciate citations to the following paper.
**Wang, G. (2022). The 95% Confidence Interval for GNSS-Derived Site Velocities, J. Surv. Eng. 2022, 148(1): 04021030. http://doi.org/10.1061/(ASCE)SU.1943-5428.0000390**
## Licence
[GNU](https://opensource.org/licenses/BSD-2-Clause)
```
Copyright (c) 2021 Brendan Cornelison, Guoquan Wang

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
this list of conditions and the following disclaimer in the documentation
and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
