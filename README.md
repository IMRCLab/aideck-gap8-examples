# AI-deck example

## About
### AI-deck
The AI-deck enables low power on-board artificial intelligence capabilities for the Crazyflie using a GAP8 chip with RISC-V multi-core architecture, 512 Mbit HyperFlash and 64 Mbit HyperRAM. In addition the deck has a Himax HM01B0 grayscale camera with a Wi-Fi module to stream your images to a desktop. These features fit the prerequites of a convolutional neural network, but the AI-deck is not limited to the application of CNN's. 

### Example
The example shows a simple convolutional neural network based on the MNIST example of the GAP8 SDK. MNIST is a CNN that classifies handwritten digits ranging from  0 to 9. If the AI-deck identifies a 0 it will send a UART byte to the Crazyflie which in turn gives a command to turn right. If it identifies a 9 it will go the left. 

This example can be easily modified to a different classification task by using a similar and simple dataset. 

## For users starting with embedded applications and the Crazyflie
For this example a basic understanding on how to:
* Program in Python and C
* Use Linux systems
* Use and editing Makefiles 

## Setting up the GAP8 SDK
To get started first set up the GAP8 SDK using the instruction on this repository:
https://github.com/GreenWaves-Technologies/gap_sdk.  


## Workflow using GAPFlow
To design a neural network and deploy it on the AI-deck, you should know the workflow of the GAP8 SDK for AI applications that is provided by GreenWaves Technologies. A neural network can be designed, trained, and evaluated using Tensorflow and Keras in Python. To let this code be able to run on the AI deck you must understand how the GAPFlow works. 

![GAPFlow](/illustrations/GAPFlow.png)
Format: ![Courtesy of GreenWaves Technologies](https://greenwaves-technologies.com/)

What you should provide in this workflow is the NNTool state file and application code programmed in C. 

### NNTool use
In this example the NNTool state file can be found in example/model/nntool_script special attention to the following command/rule 
```aquant -f 8 <image folder>/*.<image extension> -T```

The NNTool makes use of post-training quantization and adjust the quantized weights using the images defined in the aforementioned rule in the state file.


https://github.com/GreenWaves-Technologies/gap_sdk/tree/master/tools/nntool


### Autotiler use
The Autotiler supports basic operators needed for a convolutional neural network. If you need a specialized operator for your neural network, then you can make your own autotiler operator by using this page.
https://greenwaves-technologies.com/manuals/BUILD/AUTOTILER/html/index.html


## Application code for the AI-deck
### Environment
This example mainly uses the following set up. 
* FreeRTOS as OS
* PMSIS-API as driver interface
    * UART
    * Himax
* OpenOCD as debug bridge 

## Application code for the Crazyflie
### For users starting with the Crazyflie the following should be known on how to:
* Use LOG and PARAM in Crazyflie
* Make an application in the Crazyflie Applayer 