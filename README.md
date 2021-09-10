# DVC Tutorial

This is a tutorial on managing your audio datasets using [Git](https://git-scm.com/) and [DVC](https://dvc.org/). Git is a tool for keeping track of file changes. It is popular with programmers and powers sites like [GitHub](https://github.com/). Git is best is best at tracking files that contain text, like program source code. DVC is a similar tool, but is meant for larger binary files (like audio files). DVC is meant to be used in tandem with Git: you use Git to manage your small files and DVC to manage your larger binary files.

1. Make sure you have Git and DVC installed. [Install Git here](). [Install DVC here](https://dvc.org/doc/install)

2. Open up a terminal and `cd` to the root directory of your dataset. For example:

```bash
cd ~/data/LJSpeech
```

3. Initialize the Git repository:

```bash
git init
```

4. Initialize the DVC project:

```bash
dvc init
git commit -m "Initialize DVC"
```

5. Push your code up to a remote Git repository. If you use https://git.uberduck.ai to host your Git repository, you can also use Uberduck to host your DVC files!
    1. [Create a new repository](https://git.uberduck.ai/repo/create).
    2. Add the repository: `git remote add origin http://git.uberduck.ai/your-username/your-repository.git`.
    3. Push up your changes: `git push origin master`. Running this command will prompt you for a username and password. Enter your username as the username. For the password, you can [create an access token](https://git.uberduck.ai/user/settings/applications) and use that.


6. Track your audio files with DVC:

```bash
dvc add wavs/*.wav
```

This command will tell Git to ignore your `.wav` files (by adding them to `.gitignore`) and create a bunch of `.wav.dvc` files in their place. The `.wav.dvc` files are small text files that contain metadata about the original audio files. Add these new files to Git and commit.

```bash
git add wavs/*.dvc
git commit -m "Create dvc files"
```

7. Push the files tracked with DVC up to a remote DVC repository. If you're using https://git.uberduck.ai to host your Git repository, you can also use Uberduck to host your DVC files! Here is how to add and configure the DVC remote:

```bash
# Add the remote
dvc remote add -d uberduck https://api.uberduck.ai/datasets/your-username/your-repo
# Configure authentication
dvc remote modify uberduck auth basic
dvc remote modify --local uberduck user $API_KEY
dvc remote modify --local uberduck password $API_SECRET
```

`$API_KEY` and `$API_SECRET` are your Uberduck Developer key and secret. You'll soon be able to retrieve them from your [Uberduck Manage Account page](https://uberduck.ai/account/manage). Until then, ask staff in Discord to help you get an API key.

8. Push your DVC files. This command will upload your dataset, so it might take some time to complete.

```bash
dvc push
```

Congratulations! You are now storing and tracking your audio dataset with Git and DVC.