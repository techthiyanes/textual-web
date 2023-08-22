# textual-web

Textual Web is an application to publish [Textual](https://github.com/Textualize/textual) apps and terminals on the web.

Currently in a **prototype** stage (pre-beta), but available for testing.

## Getting Started

Textual Web is a Python application. But you don't need to be a Python developer to run it.

The easiest way to install Textual Web is via [pipx](https://pypa.github.io/pipx/).
Once you have pipx installed, run the following command:

```python
pipx install textual-web
```

You will now have the `textual-web` command on your path.

## Run a test

To see what Textual Web does, run the following at the command line:

```bash
textual-web
```

You should see something like the following:

<img width="1002" alt="Screenshot 2023-08-22 at 09 41 08" src="https://github.com/Textualize/textual-web/assets/554369/cc61edf8-0396-4dbc-b3b6-5573986143cd">

Click the blue link to launch the example Textual app (you may need to hold cmd or ctrl on some terminals).
Or copy the link to your browser if your terminal doesn't support links.

You should see something like this in your browser:

<img width="1058" alt="Screenshot 2023-08-22 at 09 41 35" src="https://github.com/Textualize/textual-web/assets/554369/654f670b-a90c-46e6-89df-ed3a7daabf4a">

You are seeing a simple Textual application.
This app is running on your machine, but is available via a public URL.
You could send that to anyone with internet access, and they would see the same thing.

Hit ctrl+C in the terminal to stop serving the welcome application.

## Serving a terminal

Textual Web can also serve your terminal. For quick access add the `-t` switch:

```bash
textual-web -t
```

This will generate another URL, which will present you with your terminal in your browser:

<img width="1058" alt="Screenshot 2023-08-22 at 09 42 23" src="https://github.com/Textualize/textual-web/assets/554369/1f3b0138-e724-4c90-a335-830717455c19">

When you serve a terminal in this way it will generate a random public URL.
Don't share this with anyone you wouldn't trust to have access to your terminal.

## Configuration

Textual Web can serve multiple [Textual](https://github.com/Textualize/textual) apps and terminals (as many as you like).
To do this, we need to create a TOML file.

To demonstrate this, install Textual and check out the repository.
Navigate to the examples directory and add the following file:

```toml
[app.Calculator]
command = "python calculator.py"

[app."Code Browser"]
command = "python code_browser.py"

[app.Dictionary]
command = "python dictionary.py"
```

The name is unimportant, but let's say you called it "serve.toml".
Use the `--config` switch to load the new configuration:

```bash
textual-web --config serve.toml
```

You should now get 3 links, one for each of the secions in the configuration:

<img width="1145" alt="Screenshot 2023-08-22 at 10 37 59" src="https://github.com/Textualize/textual-web/assets/554369/8e6e8248-7d77-4d77-af03-70f1a9147bf3">

Click any of the links to serve the respective app:

<img width="1131" alt="Screenshot 2023-08-22 at 10 42 25" src="https://github.com/Textualize/textual-web/assets/554369/fb4b6ad2-3431-41bc-b7b3-5cfd81e1eab8">

### Terminal configutation

You can also add a terminal to the configuration file, in a similar way.

```toml
[terminal.Terminal]
```

## Accounts

In previous examples, the URLS have all contained a random string of digits which will change from run to run.
If you want to create a permanent URL you will need to create an account.

To create an account, run the following command:


```bash
textual-web --signup
```

This will bring up a dialog in your terminal that looks something like this:

<img width="1145" alt="Screenshot 2023-08-22 at 10 49 54" src="https://github.com/Textualize/textual-web/assets/554369/539fd8bc-c218-48b9-a00f-31855e7a4306">

If you fill in that dialog, it will create an account for you and generate a file called "ganglion.toml".
At the top of that file you will see a section like the following:

```toml
[account]
api_key = "JSKK234LLNWEDSSD"
```

You can add that to your configuration file, or edit "ganglion.toml" with your apps / terminals.
Run it as you did previously:

```bash
textual-web --config ganglion.toml
```

Now the URLs generated by `textual-web` will contain your account slug in the first part of the path.
The account slug won't change, so you will get the same URLs from one run to the next.

## Debugging

For a little more visibility on what is going on "under the hood", set the `DEBUG` environment variable:

```
DEBUG=1 textual-web --config ganglion.toml
```

Note this may generate a lot of output, and it may even slow your apps down.

## What's next?

The goal of this project is to turn Textual apps into fully featured web applications.

Currently serving Textual apps and terminals appears very similar.
In fact, if you serve a terminal and then launch a Textual app, it will work just fine in the browser.
Under the hood, however, Textual apps are served using a custom protocol.
This protocol will be used to expose web application features to the Textual app.

For example, a Textual app might generate a file (say a CSV with a server report). 
If you run that in the terminal, the file would be saved in your working directory.
But in a Textual app it would be served and saved in your downloads folder, like a regular web app.

## Help us test

Currently testing is being coordinated via our [Discord server](https://discord.com/invite/Enf6Z3qhVr).
Join us if you would like to participate.
