---
layout: page
title: Development with the RP2040
---

# An introduction to C++ development with the RP2040

The RP2040 is a multipurpose microcontroller, and is our go-to chip on rocketry. It's a 32-bit dual core ARM processor (Cortex-M0 &micro;architecture). We use C++ with the RP2040 on rocketry; however, it also supports CircuitPython. For more information on using CircuitPython with the RP2040, I'd suggest taking a look at [_Raspberry Pi Pico Python SDK_](https://g.cornellrocketryteam.com/rp2040-py)

## Installing the RP2040 C++ Toolchain

These instructions vary by operating system.

### MacOS

First, make sure that you have the command line developer tools. Run
`xcode-select --install` and agree to the prompt.

If you don't have [Homebrew](https://brew.sh), install it:
```sh
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once Homebrew is installed, you can use it to install the ARM toolchain:

```sh
$ brew install cmake
$ brew tap ArmMbed/homebrew-formulae
$ brew install arm-none-eabi-gcc
```

Next, you need to install the Pico SDK. You can install this wherever you want, but these directions assume you're going to install it at `~/pico`.

```
$ mkdir ~/pico
$ cd ~/pico
$ git clone -b master https://github.com/raspberrypi/pico-sdk.git
$ cd pico-sdk
$ git submodule update --init
```

TODO: instructions on setting `export PICO_SDK_PATH=../../pico-sdk`

### Configuring Visual Studio Code

First, install the 

## Blink

Traditionally, the first program you write to test something is a "Hello, World!" program, which prints `Hello, World!` to the scrren. When you're writing code for hardware, the equivalent of that is the Blink program, where you simply blink an LED forever.

Let's write a blink program.

We need to start by creating a CMake file, which specifies how the program should be built. Create a new directory, and in that directory, create a file called `CMakeLists.txt`.

Add the following content to the file:

{% include note.html content="Protip: Retype, rather than copying and pasting. This helps you think about everything you type, rather than saying \"yeah that makes sense\" and moving on." %}

```cmake
# Specify the minimum required CMake version
cmake_minimum_required(VERSION 3.13)

# Include the pico_sdk_import
include(pico_sdk_import.cmake)

# Define your project 
project(blink_project C CXX ASM)

# Set your C and C++ Standards 
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initalize the Pico SDK
pico_sdk_init()

# Add the blink executable
add_executable(blink blink.c)

## Setup external stdio (USB/UART)
## We won't use it here, but I put it for the sake of example
# pico_enable_stdio_usb(blink 1)
# pico_enable_stdio_uart(blink 1)
# pico_add_extra_outputs(blink)

# Link blink against the Pico standard library
target_link_libraries(blink pico_stdlib)
```

Next, let's write a simple "blink" program.
```cpp
// First, we include the Pico's standard library.
#include "pico/stdlib.h"


int main() {
	// Pins are represented as an unsigned integer
	// The defualt LED pin is 25.
	const uint BLINK_PIN = PICO_DEFAULT_LED_PIN;

	// Each blink will last this amount of time (in ms).
	const int BLINK_DURATION = 500;

	// Initalize the blink pin for general purpose input/output (GPIO)
	gpio_init(BLINK_PIN);

	// Use the blink pin as a digital output
	gpio_set_dir(BLINK_PIN, GPIO_OUT);

	while(true) {
		// set the blink pin high		
		gpio_put(BLINK_PIN, 1);
		// spend half the time with the LED on.
		sleep_ms(BLINK_DURATION/2);
		// set the blink pin low
		gpio_put(BLINK_PIN_0);
		// spend half the time with the LED off.
		sleep_ms(BLINK_DURATION/2);
	}

	#endif
}
```