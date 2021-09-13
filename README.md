# DVC Tutorial

This is a tutorial on managing your audio datasets using [Git](https://git-scm.com/) and [DVC](https://dvc.org/). Git is a tool for keeping track of file changes. It is popular with programmers and powers sites like [GitHub](https://github.com/). Git is best is best at tracking files that contain text, like program source code. DVC is a similar tool, but is meant for larger binary files (like audio files). DVC is meant to be used in tandem with Git: you use Git to manage your small files and DVC to manage your larger binary files.

1. Make sure you have Git and DVC installed. [Install Git here](). [Install DVC here](https://dvc.org/doc/install)

2. Go to the [`tts-dataset-template`](https://git.uberduck.ai/zwf/tts-dataset-template) and click "Use this template". Give your dataset a name and short description, and make sure `Git Content (Default Branch)` is checked at the bottom under `Template Items`. Then create the repository.

3. Clone your newly created repository. Running this command will prompt you for a username and password. Enter your username as the username. For the password, you can [create an access token](https://git.uberduck.ai/user/settings/applications) and use that.

```bash
git clone https://git.uberduck.ai/your-username/Your-Repo.git
cd Your-Repo
```

4. Track your audio files with DVC (assuming they are in a directory called `wavs`):

```bash
dvc add wavs
```

This command will tell Git to ignore everything inside the `wavs` directory and create a `wavs.dvc` file in its place. The `wavs.dvc` file is a small text file that contains metadata about the directory and its contents. Add this file to Git and commit.

```bash
git add wavs.dvc
git commit -m "Add dvc file"
```

5. Push the files tracked with DVC up to a remote DVC repository. If you're using https://git.uberduck.ai to host your Git repository, you can also use Uberduck to host your DVC files! You need an Uberduck API key and API secret, which you can create on your [Uberduck Manage Account page](https://uberduck.ai/account/manage). Once you have the key and secret, configure the DVC remote:

```bash
# Authenticate to DVC
dvc remote modify --local uberduck user $API_KEY
dvc remote modify --local uberduck password $API_SECRET
```

6. Push your DVC files. This command will upload your dataset, so it might take some time to complete.

```bash
dvc push
```

Congratulations! You are now storing and tracking your audio dataset with Git and DVC. You can see an example dataset which was created with this tutorial at [LJSpeech-example](https://git.uberduck.ai/zwf/LJSpeech-example).