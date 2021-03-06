Process Management for NodeJS
=============================

This module provides advanced facilities for querying and manipulating running
processes on macOS and Linux. It does so by integrating with the relevant
routines provided by the OS.

:warning: Windows is not (yet) supported.

### Features

 - Query whether any process is running, even daemons and non-GUI applications on macOS.
 - Connect to a process and be notified when it is done.
 - Send a custom signal to a process
 - Kill a process

Pull requests are welcome!

## Example

**wait-until-exit.js**
```js
#!/usr/bin/env node

import { Process } from "procman"

const pid = Number(processes.argv[2])

if (isNaN(pid)) {
  console.error('Not a valid PID.')
  process.exit(1)
}

const myProc = new Process(pid)

myProc.on('exit', () => {
  console.log('The process has exited.')
})
```

## API

### new Process(pid)

Connects to the given process indicated by the PID number and waits for it to
exit. NodeJS will be forced to keep running until the process exits or
`Process.close()` is explicitly called.

### Process.running

Indicates whether the given process is running **right now**. This value might
change even during the same execution context.

### Process.on('exit', callack)

Registers a callback to be executed when the process exits.

### Process.close()

Stops monitoring the process and allows NodeJS to exit.

### Process.kill(signal?)

Send the given signal to the process.

If no signal is provided, will default to `SIGTERM`.

## License

The code is licensed under the MIT license, which means you may use it in
commercial products as long as you retain the copyright information.

