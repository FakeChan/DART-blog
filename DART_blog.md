## Observations

DART里面有一系列的观测，例如``RADIOSONDE_U_WIND_COMPONENT``。但是在默认设置里面没有卫星亮温观测，需要自己添加。在``${DART_dir}/observations/forward_operators``中可以找到自己需要的观测类型，例如``obs_def_rttov_mod.f90``就是使用RTTOV计算的卫星亮温观测。在``${DART_dir}/models/${your_model}/work``中修改``input.nml``中的``&preprocess_nml``，添加``obs_def_X_mod.f90``，执行``preprocess``程序即可更新观测类型。此时在``${DART_dir}/assimilation_code/modules/observations``中的``obs_kind_mod.f90``中可查看同化的观测在DART中的代号。例如，``NOAA_18_AMSUA_TB =   170``。

**如果需要添加新观测，例如linfan和haoxing使用的FY4A-GIIRS，只需在``obs_def_rttov_mod.f90``中的*注释*部分添加观测类型，即`FY4_1_GIIRS_TB,               QTY_BRIGHTNESS_TEMPERATURE**`

### 2025.3.20
今天知道了为什么要这样弄obs...DART不支持RTTOV12.3之前的版本，编译DART+RTTOV的时候得专门装一个RTTOV12.3来满足环境

### 2025.4.14
DART localization : vertical localization radius = 2 * cutoff * vert_normalization_height
### 2025.4.23
如果需要在wrf_state_variables里面添加新的需要更新的变量，需要在model_mod.f90中static_init_model模块自行添加


## localization
ocean vars在WRF-DART里面的垂直坐标没有默认的读入，需要在model_mod里面自行更改，位置处于``model_height_distrib``这个子程序中。
