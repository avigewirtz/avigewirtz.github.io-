# Understanding each stage

## How Information is Represented in Computers

At its core, all information in computers is stored as a sequence of bits, which represent one of two states of the underlying electrical or magnetic states of the computer's memory components. For simplicity we represent these two states using 1s and 0s. For instance, a memory cell may consist of a tiny capacitor and transistor. A charged capacitor represents a 1, while a discharged capacitor signifies a 0. Alternatively, magnetic polarities of magnetic material may denote both states, with one polarity corresponding to a 1 and the opposite polarity to a 0.

All information, such as numbers, images, audio, videos, and executable programs are stored as sequences of 1s and 0s. You might be wondering how a sequence of 1s and 0s can represent such complex information. The answer is we use encoding schemes. For example, we represent signed integers using twos complement, floating point numbers using a standard called the IEEE 754 floating-point standard, and we represent text using an encoding scheme such as ASCII or unicode.&#x20;



<details>

<summary>A brief overview of how computers represent images, audio, and video</summary>

* Images: Images are represented as a matrix of pixels, where each pixel corresponds to a specific color. The color information is represented using various color models, such as RGB (Red, Green, Blue) or CMYK (Cyan, Magenta, Yellow, Key/Black). Each color channel is represented by a specific number of bits, which determines the range of color values that can be represented.

<!---->

* Audio: Audio data is typically represented as a continuous waveform, which is then sampled at regular intervals to create a digital representation. Each sample represents the amplitude of the waveform at a specific point in time, and the samples are stored using various audio formats and encoding techniques.

<!---->

* Video: Video data is essentially a sequence of images (frames) displayed over time. Each frame is represented using image data formats, and the sequence of frames is stored using various video encoding and compression techniques to reduce the file size while maintaining an acceptable level of quality.

</details>
