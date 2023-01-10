# gpt-cli

This is a command line tool used for interacting with OpenAI's API.

Default model is `text-davinci-003` (which ChatGPT was originally built from).

This tool requires the following environment variables to be set:

- `OPENAI_API_KEY`
- `OPENAI_ORGANIZATION_ID`

You can further tweak functionality by setting the following additional environment variables:

- `OPENAI_MODEL`
- `OPENAI_DEFAULT_PROMPT`
- `OPENAI_LOGFILE`
- `OPENAI_TEMPERATURE`
- `OPENAI_MAX_TOKENS`

All environment variables can be set by filling in values from `example.env`, renaming that file to `.env`, and running `./bin/gpt 'Your prompt here'`.

Alternately, you can pass them all on the command line using something like this:

```
OPENAI_API_KEY=foo OPENAI_ORGANIZATION_ID=bar ./bin/gpt 'Your prompt here'
```

If installing from PyPi, set the `OPENAI_API_KEY` and `OPENAI_ORGANIZATION_ID` in your `~/.bashrc` or `~/.zshrc`, and run as follows:

```
gpt 'Your prompt here'
```

## Installation (PyPi) - set variables in rc files:

`python3 -m pip install gpt-cli`

## Installation (local) - set variables in .env:

```
git clone https://github.com/phx/gpt-cli
cd gpt-cli
python3 -m pip install -r requirements.txt
```

