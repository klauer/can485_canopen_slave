AST-CAN485 CANopen Slave Example
--------------------------------

A simple CANopen slave example using the SparkFun AST-CAN485 board.

Connections
-----------

4 digital inputs and 8 digital outputs are exposed through PDOs as follows:

| AST-CAN485    | Port / bit    | Usage          | CANopen         |
|:-------------:|:-------------:|:--------------:|:---------------:|
| A0            | PF0           | Input / TxPDO  | 0x6000:01 bit 0 |
| A1            | PF1           | Input / TxPDO  | 0x6000:01 bit 1 |
| A2            | PF2           | Input / TxPDO  | 0x6000:01 bit 2 |
| A3            | PF3           | Input / TxPDO  | 0x6000:01 bit 3 |
| RXI           | PE0           | Output / RxPDO | 0x7000:01 bit 0 |
| TXO           | PE1           | Output / RxPDO | 0x7000:01 bit 1 |
| D4            | PE2           | Output / RxPDO | 0x7000:01 bit 2 |
| D5            | PE3           | Output / RxPDO | 0x7000:01 bit 3 |
| D6            | PE4           | Output / RxPDO | 0x7000:01 bit 4 |
| D7            | PE5           | Output / RxPDO | 0x7000:01 bit 5 |
| D8            | PE6           | Output / RxPDO | 0x7000:01 bit 6 |
| D9            | PE7           | Output / RxPDO | 0x7000:01 bit 7 |


Standard output (stdout) and standard error (stderr) can be used directly with
the Arduino FTDI serial port monitor at 9600 baud.

A 120 ohm resistor should be connected between CANL and CANH, as noted in the 
hookup guide.  For connecting to a Beckhoff EL6751 / Dsub9 CANopen master:

| AST-CAN485    | EL6751 DB9    |
|:-------------:|:-------------:|
| CANLO         | Pin 2         |
| CANHI         | Pin 7         |
| GND           | Pin 3 / Pin 6 |

Object Dictionary
-----------------

The CANopen object dictionary is provided as both `.od` and `.eds` (what
Beckhoff TwinCAT3 expects).

Building
--------

The provided `Makefile` and Atmel Studio 7 project should work directly.

Uploading
---------

A couple tweaks to the Makefile:
    1. Change the `ARDUINO_ROOT` path to point to where you have it installed
    2. Change the `COM_PORT` to the appropriate device
    
Will also allow you to upload using `avrdude` like so:

```bash
$ make all upload
```

CANopen library
---------------

This repository, in the interests of making a focused and easily compilable
example for the AST-CAN485, includes a vendored copy of `canfestival-3-asc`.

It currently corresponds with the changeset `968:1a25f5151a8d` (2018/5/11) from
its bitbucket hg repository.

Python
------

Located in `canfestival/objdictgen`:

The object dictionary editor program, based on wxPython, still runs on Python 2.7.
It requires wxPython 3, which is not available via pip. 

To get this working with conda:
```bash
$ conda create -n canfestival python=2.7 wxpython==3
$ cd canfestival/objdictgen
$ source activate canfestival
$ pythonw objdictedit.py ../../ObjDict.od
```

Links
-----
* [canfestival-3-asc repository](https://bitbucket.org/Mongo/canfestival-3-asc)
* [AST-CAN485 product page](https://www.sparkfun.com/products/14483)
* [AST-CAN485 schematic](https://cdn.sparkfun.com/assets/2/8/3/4/7/SparkFun_AST-CAN485.pdf)
* [AST-CAN485 hookup guide](https://learn.sparkfun.com/tutorials/ast-can485-hookup-guide/)
