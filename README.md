# How to Disable WebAssembly (WASM)

WebAssembly (WASM) is an effort to increase performance of in-browser Javascript execution by introducing a 
highly-optimized binary format that executes at near-native speed. The potential of WASM is quite exciting
with enoumous potential. All major browser vendors have enabled WebAssembly by default.

## Security Considerations

WebAssembly increases the attack surface of any browser that supports it. In security engineering, countermeasures
are typically employed to reduce risk to potential threats. Here are a few concerning aspects of WebAssembly:

* Web server sends WASM modules to browser in binary format
* WebAssembly execution relies on browser sandboxing for safety
* Transmission  and execution does not require TLS, HSTS, or any other transport layer security mechanism
* Integrity checking is not possible as WASM modules are not required to be signed by their author
* A primary  WebAssembly goal is to: *provide developers with useful primitives and mitigations for developing safe applications*.

Based on the above facts, here are some potential threats in using browsers that support WebAssembly:

* Static code analysis becomes increasingly difficult as source code may not be available
* Sandboxing is prone to breakouts and effectiveness varies largely by implementation. Adobe Flash is an 
example of a technology that was sandboxed after a series of exploits, yet exploits and breakouts still occurred.
* Transmitting a binary executable format over an insecure channel is susceptible  to man-in-the-middle attack. 
* Code signing, the process of verifying software has not been tampered with, is not currently possible with WASM.
WASM is selling itself as the ability to run desktop-like applications in the browser, yet the operating systems
it supports all have code signing requirements for installed software. Allowing random drive-by software to execute
unsigned seems to be a 'feature' of WebAssembly.
* WebAssembly assumes that 'safe applications' can be derived from language subsets and a few rules to prevent 
specific type of behavior. This is similar to blacklisting in the security world, a technique that rarely works.
The specification omits the possibility of misuse cases from their security dialog. Exploits can occur in 'safe applications'
simply by using the application in a way it wasn't designed to run. Since static code analysis is not currently 
possible, automatically identifying potential performance, insider-threats, security, and misuse cases is not possible.

The WebAssembly specification does not address any of the above threats. Therefore, I have disabled WASM on my personal 
browsers and have discountinued use of browsers that do not allow WASM to be disabled. To be fair, many of the threats 
above also apply to Javascript, which **can** be statically analyzed or outright disabled.

## How to Disable WebAssembly

**Edge**

Unknown. I do not use Windows so if someone knows the answer to this, please submit a pull request.

**FireFox**

Enter about:config in the URL bar and change javascript.options.wasm to false

**Chrome**

Enter chrome://flags/#enable-webassembly in the URL bar and change value to Disabled.

**Brave**

about:config functionality is not yet implemented, therefore, it is not possible to disable WASM at this time. 
An enhancement request is proposed to provide Chrome-like flags. Refer to https://github.com/brave/browser-laptop/issues/545

**Safari**

Safari does not have advanced about:config functionality and the Developer mode does not have an option to 
disable WASM.
