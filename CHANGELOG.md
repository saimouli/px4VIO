# Change Log
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## [Unreleased]
### Changed
- Replaced original ATLFlight README with a link.

## 0.0.2 - 2017-06-1
### Changed
- EKF2 now using vision as main source for height estimation instead of the barometer. Height estimate is now as good as `X` and `Y` estimations.
- Added px4 configuration files to run LPE estimator instead of EKF2. Seems to work better than EKF2 as anticipated in the [official documentation](https://dev.px4.io/en/ros/external_position_estimation.html)

## 0.0.1 - 2017-06-1
### Changed
- VISLAM running with IMU measurements coming from mavros

### Added
- EKF2 sensor fusion of VISLAM odometry on px4. `Z` is a bit doing whatever it wants (I guess baro) and occasionally the ekf2 output jumps to zero for one time step before it recovers. 
- px4 configuration files for snapdragon added to `./px4_confs`.
