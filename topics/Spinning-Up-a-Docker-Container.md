# Spinning Up a Docker Container
<p>
    Now that you've got OrbStack open, head over to your terminal. If you type <code>docker run -it --rm {lang}</code>, where <code>{lang}</code> is the language you are working with,
    you'll spin up a docker container with the specified language's console.</p>
<p>
    There's a few parts to this command. We'll break them down using 
</p>
<code-block lang="docker">
    docker run -it --rm ruby:3.3
</code-block>
<list type="bullet">
    <li>`docker` - This is the starting point for Docker CLI commands.</li>
    <li>`run` - The docker run command runs a command in a new container, pulling the image if needed and starting the container.</li>
    <li>`-it` - This flag on the command is for `-interactive`, meaning it'll pull you straight into the console of the container after creating it.</li>
    <li>`--rm` - This flag automatically removes the container and its associated anonymous volumes when it exits - meaning you won't leave unused containers chilling and taking up resources.</li>
    <li>`ruby:3.3` - This is where you're specifying which language (and version) you need in the container.</li>
</list>
<p>
    So in this case, you're telling your terminal to use docker to start a Ruby v3.3 container, move into its console, and delete the container when you exit it.
</p>
<tip>There's many other docker commands you can find in their <a href="https://docs.docker.com/reference/cli/docker/">CLI documentation.</a></tip>

<chapter title="Bonus Tip: `alias`" id="alias" collapsible="true">
    You can use `alias` in your <code>~/.zshrc</code> file to shorten commonly used commands.
    <list type="decimal">
        <li>Navigate to your home directory. (You can shortcut this by using just <code>cd</code> without an argument on the command line)</li>
        <li>Use <code>sudo nano ~/.zshrc</code>, which will ask for your password (the password to your computer)</li>
        <li>Scroll down to the bottom of the text, and on a new line add <code>alias {command}="docker run -it --rm"</code>.</li>
        <li>Replace {command} with whatever shorthand you want to use.</li>
        <li>Press <code>control+o</code> followed by <code>return</code>to write the file, saving changes.</li>
        <li>Press <code>control+x</code> to exit out of the file.</li>
        <li>Run <code>source ~/.zshrc</code> on the command line to "restart" your terminal, allowing your changes to take effect</li>
        <li>Use your new command!</li>    
    </list>
    To abstract in the simplest way possible, this is the same as setting a "text replacement" on your device. You are giving a command a sort of nickname, so for example:
    <code-block>alias rubyenv="docker run -it --rm ruby:3.3"</code-block>
    With this in my zshrc file, I can then type <code>rubyenv</code> right on the command line and hit enter, performing this whole command without needing to type it out.
    This is not tied to any service beyond your terminal, so you can use it to shorten all kinds of commonly used commands.
    <tip>
        Since this is a text replacement and not the full command, you can easily add arguments. This means if I omit the <code>ruby:3.3</code> portion, I could instead do <code>rubyenv ruby:3.3</code>
        allowing me to use various languages with that same command (even though the name then doesn't make sense).
    </tip>
    <warning>
        If you get an error talking about permissions when using your first alias, you may need to set the ownership of your zshrc file correctly. You can do this via 
        <code>chmod 644 ~/.zshrc</code> followed by another <code>source ~/.zshrc</code>.
    </warning>
</chapter>

