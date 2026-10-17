> ## Fork notice
>
> This is **our fork** of [`shajen/rtl-sdr-scanner-cpp`](https://github.com/shajen/rtl-sdr-scanner-cpp)
> (GPLv3) - the C++ GNU Radio/SoapySDR scanner that runs inside `sdr-hub`.
> Maintained by **Jim Gifford**. **Updates are made both manually and with AI
> assistance** (DevPass Code); every change is reviewed, compiled against the
> production runtime image and tested before it is deployed.
>
> ### Changes vs upstream
> - **No more missing recordings / `time: 0 ms`** - `Signal::needFlush()`
>   requested a flush only on the exact tick of a signal's last data point, so
>   anything that dipped below the stop level was never flushed (upstream
>   issue #132).
> - **No tail loss** - buffered audio is flushed when a recorder is dropped and
>   once more in its destructor.
> - **`Recording::flush` defaults to `false`** (it was an uninitialized bool).
> - **Honest source labels** - spectrograms and transmissions are published as
>   `scanner` instead of the hard-coded `gain tester` label upstream uses when a
>   device alias is set.
> - **Processor cap** - more than 32 range processors are skipped with a warning
>   instead of overloading the host (upstream issue #107).
>
> ### Credit and acknowledgements
> - **shajen** - the original scanner and `sdr-hub`
>   (<https://github.com/shajen/rtl-sdr-scanner-cpp>,
>   <https://github.com/shajen/sdr-hub>, <https://shajen.pl>). Without their
>   work this fork would not exist.
> - **The upstream issue reporters** whose reports identified these bugs:
>   #132 "No recordings ?", #118 "No way for user to enable direct sampling",
>   #127 "Compatibility with RTL SDR Blog v4", #107 "Multiple ranges causes
>   problems".
> - **rtlsdrblog/rtl-sdr-blog** - RTL-SDR Blog V3/V4 driver enhancements used by
>   the dongles this fork serves.
> - **GNU Radio**, **SoapySDR** and **Paho MQTT** - the libraries it is built on.
>
> License: GPL-3.0, unchanged from upstream - see [LICENSE](LICENSE).

# Introduction

This project is part of a larger `SDR` project called [https://github.com/shajen/sdr-hub](https://github.com/shajen/sdr-hub). Please familiar with it before starting work.

This project contains sdr scanner written in `c++` to **scan and record multiple interesting frequencies bandwidth in the same time** (eg. 108 MHz, 144 MHz, 440 Mhz,  etc). This is possible by switching quickly between frequencies bandwidth.

Sdr scanner also allows you to record multiple transmissions simultaneously (if they are transmitted on the same band). For example, if one transmission is on 145.200 MHz and the other is on 145.600 MHz, the scanner will record and save both!

# Supported devices

Sdr scanner use [SoapySDR](https://github.com/pothosware/SoapySDR) library to get data so it support all devices that are supported by `SoapySDR`. Full list of supported devices [here](https://github.com/pothosware/SoapyOsmo/wiki).

# Quickstart

Instructions [here](https://github.com/shajen/sdr-hub?tab=readme-ov-file#quickstart).

# Build from sources

Clone repository and run:
```
docker build -t shajen/sdr-scanner .
```

# Contributing

In general don't be afraid to send pull request. Use the "fork-and-pull" Git workflow.

1. **Fork** the repo
2. **Clone** the project to your own machine
3. **Commit** changes to your own branch
4. **Push** your work back up to your fork
5. Submit a **Pull request** so that we can review your changes

NOTE: Be sure to merge the **latest** from **upstream** before making a pull request!

# Donations

If you enjoy this project and want to thanks, please use follow link:

- [PayPal](https://www.paypal.com/donate/?hosted_button_id=6JQ963AU688QN)

- [Revolut](https://revolut.me/borysm2b)

- BTC address: 18UDYg9mu26K2E3U479eMvMZXPDpswR7Jn

# License

[![License](https://img.shields.io/:license-GPLv3-blue.svg?style=flat-square)](https://www.gnu.org/licenses/gpl.html)

- *[GPLv3 license](https://www.gnu.org/licenses/gpl.html)*
