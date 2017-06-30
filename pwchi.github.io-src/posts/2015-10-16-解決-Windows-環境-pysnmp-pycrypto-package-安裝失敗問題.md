<!--
.. title: 解決 Windows 環境 pysnmp / pycrypto package 安裝失敗問題
.. slug: 解決 Windows 環境 pysnmp / pycrypto package 安裝失敗問題
.. date: 2015-10-16 16:44:02 UTC+08:00
.. tags: Python
.. category:
.. link:
.. description:
.. type: text
-->
* Windows 7 x64
* Python 3.4

今天執行 `pip install pysnmp` 時一直出現下面的錯誤訊息，問題似乎出在其中一個相依套件 **pycrypto** 。

```
building 'Crypto.Random.OSRNG.winrandom' extension
warning: GMP or MPIR library not found; Not building Crypto.PublicKey._fastmath.
error: Unable to find vcvarsall.bat
```

原因是 Windows 環境需要 VC 去編譯 winrandom ，我沒有 VC 自然會失敗收場。

解決辦法是去下載並安裝人家已經編譯好的 pycrypto 二進位安裝檔，就能順利執行 `pip inatall pysnmp` 了。

PS. 目前尚未有對應 Python 3.5 的安裝檔，所以需要 pycrypto 套件的話先別上 Python 3.5。

適用 Python 3.4

* [https://github.com/axper/python3-pycrypto-windows-installer](https://github.com/axper/python3-pycrypto-windows-installer)

適用 Python 2.x-3.3

* [http://www.voidspace.org.uk/python/modules.shtml#pycrypto](http://www.voidspace.org.uk/python/modules.shtml#pycrypto)
