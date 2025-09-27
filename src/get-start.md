# Getting started

The labs for ETC2073 Artificial Intelligence will be using Python as the programming language. The Anaconda distribution of Python is recommended, however, if you are familiar and comfortable with the vanilla distribution of Python. For those who have not installed Python in their machine, proceed to [next session](#installation). This page only covers the installation of the Anaconda platform as, in my opinion, it is more beginner friendly in terms of installing packages and encapsulating environments.

## Installation

1. Download the Anaconda installer with Python 3 for your system from [https://www.anaconda.com/download](https://www.anaconda.com/download).

2. Use the graphical installer to install Anaconda.


## Launching IDE

You will be using the Spyder IDE for Python. Feel free to use other IDE or code editor with terminal if that's your preference.

<div style="text-align: center"><svg xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="xMidYMid meet" width="126" height="40" class=""><path fill="#303030" class="fill-mine-shaft-950 dark:fill-white" d="M124.9 14.564c.341.103.512.24.512.58v1.436a.44.44 0 0 1-.546.478h-2.98c-2.357 0-2.972.376-2.972 1.917v13.57a.454.454 0 0 1-.512.512h-2.22a.454.454 0 0 1-.517-.512v-14.35c0-3.86 3.417-3.996 5.402-3.996.82-.01 3.15.123 3.833.365zm-12.92 8.64v.99c0 .684-.172.96-1.23.96H99.877c.103 4.169.892 5.194 4.547 5.194h5.607a.454.454 0 0 1 .512.512v1.507a.506.506 0 0 1-.478.547 42.302 42.302 0 0 1-5.709.307c-6.426 0-7.793-1.882-7.793-9.504s1.367-9.536 7.793-9.536c6.119.007 7.554 1.818 7.622 9.023zm-12.136-.717h8.855c-.068-4.343-.785-5.436-4.342-5.436-3.69.004-4.445 1.1-4.513 5.443zM91.918 7.215a.454.454 0 0 1 .512.513v24.359c0 .376-.204.512-.546.546a38.506 38.506 0 0 1-7.11.581c-6.634 0-7.967-1.882-7.967-9.47 0-7.588 1.333-9.566 7.793-9.566a36.525 36.525 0 0 1 4.547.24v-6.69a.454.454 0 0 1 .513-.513Zm-7.113 9.84c-4.236 0-4.715 1.298-4.715 6.665 0 5.265.445 6.631 4.684 6.631a38.038 38.038 0 0 0 4.373-.273V17.055Zm-12.678-2.696a.454.454 0 0 1 .512.513v16.473c-.034 6.703-1.332 8.65-7.895 8.65a34.355 34.355 0 0 1-5.162-.307.506.506 0 0 1-.478-.546v-1.473a.454.454 0 0 1 .512-.512h5.06c3.826 0 4.684-.923 4.684-3.998v-.204a26.948 26.948 0 0 1-4.513.273c-6.46 0-7.827-1.95-7.827-9.334v-9.022a.454.454 0 0 1 .512-.513h2.22a.454.454 0 0 1 .513.513v8.817c0 5.333.547 6.666 4.783 6.666a36.863 36.863 0 0 0 4.308-.24V14.872a.454.454 0 0 1 .513-.513zm-19.074 9.33c0 7.622-1.366 9.539-7.827 9.539a37.498 37.498 0 0 1-4.513-.205v6.29a.454.454 0 0 1-.512.512h-2.255a.454.454 0 0 1-.513-.513V15.346c0-.375.205-.512.547-.58a38.134 38.134 0 0 1 7.075-.581c6.632.003 7.998 1.95 7.998 9.504zm-12.34-6.634v13.023a36.979 36.979 0 0 0 4.308.273c4.24 0 4.752-1.298 4.752-6.631s-.478-6.665-4.683-6.665z"></path><path fill="#303030" class="fill-mine-shaft-950 dark:fill-white" d="M32.514 14.496a.506.506 0 0 1 .478.546v1.47a.454.454 0 0 1-.512.512h-6.358c-1.575 0-2.498.547-2.498 1.776v.448c0 .957.445 1.776 2.122 2.391l4.544 1.811c3.146 1.196 3.416 2.942 3.416 4.82v.376c0 3.83-2.292 4.582-6.904 4.582-2.976 0-5.675-.24-6.256-.308-.41-.034-.512-.239-.512-.512V30.9a.454.454 0 0 1 .512-.512h6.324c2.733 0 3.587-.308 3.587-1.777v-.41c0-.99-.41-1.64-1.981-2.289l-4.855-1.848c-2.63-1.025-3.28-3.006-3.28-4.885v-.721c0-3.758 3.28-4.27 6.939-4.27a43.3 43.3 0 0 1 5.234.307z"></path><path fill="#8c0000" class="fill-red-berry-900 dark:fill-white" d="M30.857 1.27A5.65 5.65 0 0 0 27.283 0H5.678a5.63 5.63 0 0 0-2.644.656A5.73 5.73 0 0 0 .738 2.88a5.04 5.04 0 0 0-.28.56c-.048.13-.106.257-.15.383a5.234 5.234 0 0 0-.205.796A5.466 5.466 0 0 0 0 5.681v21.606a5.593 5.593 0 0 0 .56 2.46 5.678 5.678 0 0 0 5.125 3.21h11.523a.304.304 0 0 0 .308-.303v-1.367a.307.307 0 0 0-.308-.307h-1.496l-4.465-9.06L21.445 8.415a1.141 1.141 0 0 0 .188-.397l9.337 1.428v2.101a.31.31 0 0 0 .307.308h1.387a.307.307 0 0 0 .304-.308V5.678a5.647 5.647 0 0 0-2.111-4.407zm-11.76.725.482 3.847-7.546-1.155-.342-2.692Zm-13.419 0H9.83l.297 2.392-5.504-.827-1.742-.27a3.662 3.662 0 0 1 2.798-1.295Zm4.202 4.23-3.85 5.124-3.034-6.183Zm-7.885 1.09 2.467 4.998-2.467.304Zm0 7.174 3.324-.42 3.444 6.973-6.768.85zm11.667 16.49H5.986a4 4 0 0 1-3.99-4.017V23.72l7.621-.957Zm-3.324-10.89-3.416-6.895 5.005-6.628 7.714 1.182Zm20.625-12.49-9.498-1.477-.516-4.137h6.027a4 4 0 0 1 3.987 4z"></path></svg>
</div>

1. Start the Anaconda Navigator from your application list.

2. From Anaconda `base` environment, launch Spyder IDE.

3. The Spyder IDE consists of three parts: the editor, the variable explorer, and the IPython Console.

4. The editor is where you write your codes.

5. The variable explorer shows the value of the variable after running the code.

6. The IPython console allows you to execute commands, interact with the running code, and display visualisation.

7. After the code is written in the editor, you can execute the code using <kbd>F5</kbd> to run file.

8. Then the variables and their values can be found in the variable explorer.




<!-- :::: tabs

::: tab Windows
``` bash
python 
```
:::


::: tab Mac
``` javascript
() => {
  console.log('Javascript code example')
}
```
:::

::: tab Linux

:::

:::: -->
