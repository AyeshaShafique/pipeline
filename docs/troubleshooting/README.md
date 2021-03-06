# Troubleshooting

## PipelineAI 24x7 Support
* Slack:  [![PipelineAI Slack](http://pipeline.ai/assets/img/slack.png)](https://joinslack.pipeline.ai)
* Email:  help@pipeline.ai
* Web:  https://support.pipeline.ai
* Troubleshooting:  [Guide](/docs/troubleshooting)

## Install Tools
* [Docker](https://www.docker.com/community-edition#/download)
* Python 2 or 3 ([Conda](https://conda.io/docs/install/quick.html) is Preferred)
* (Windows Only) [PowerShell](https://github.com/PowerShell/PowerShell/tree/master/docs/installation)

## GPUs
* For GPU-based models, make sure you specify `--model-chip=gpu` or `--start-cmd=nvidia-docker` where appropriate 
* For GPU-based models, sure you have `nvidia-docker` installed!

## Gathering More Information
* If your server starts, try running `pipeline predict-server-logs` or `pipeline train-server-logs` to collect the startup logs.
* Please send all relevant information to PipelineAI [Support](#pipelineai-24x7-support) (Slack, Email, or Web).

## UnicodeDecodeError: 'ascii' codec can't decode byte 0xa0 in position 40: ordinal not in range(128)
* You likely have a pickling issue.
* Make sure that you are using Python 3.  We see issues when training on Python 2 (your environment), then unpickling with Python 3 (PipelineAI Model Runtime Environment)
* Also, we've found the `cloudpickle` library to be the most stable (versus Python's default `pickle` and `dill`.)

## WARNING: Your kernel does not support swap limit capabilities or the cgroup is not mounted. (`*-start`)
* Just ignore this

## `localhost:<port>` Not Working
* Instead of `localhost`, you may need to use `192.168.99.100` or another IP/Host that maps to your local Docker host.  
* This usually happens when using Docker Quick Terminal on Windows 7.

## PermissionError: [Errno 13] Permission denied: '...'
* Likely an issue installing the PipelineCLI 
* The cli requires Python 2 or 3 - preferably [Miniconda](https://conda.io/docs/user-guide/install/index.html#id2)
* Try `sudo pip install ...`
* Try `pip install --user ...`

## Could not delete '/usr/local/lib/python3.5/dist-packages/markupsafe/_speedups.cpython-35m-x86_64-linux-gnu.so': Permission denied
* Try `sudo pip install ...`

## Latest PipelineCLI Version is Not Installing Properly
* You need Python 2 or 3 (Conda Preferred)
* (Windows Only) [PowerShell](https://github.com/PowerShell/PowerShell/tree/master/docs/installation) 

```
pipeline version

### EXPECTED OUTPUT ###
cli_version: 1.5.xx <-- Exact Version You Are Expecting
```
```
sudo pip uninstall cli-pipeline
```
```
which pipeline
``` 
(or otherwise find which `pipeline` binary is being used.)
```
rm <bad-version-of-pipeline>
```
```
ll /usr/local/lib/python3.6/dist-packages/cli-pipeline*
```
```
rm -rf /usr/local/lib/python3.6/dist-packages/cli-pipeline*
```
```
ll ~/.local/lib/python3.6/site-packages/cli_pipeline*
```
```
rm -rf ~/.local/lib/python3.6/site-packages/cli_pipeline*
```
* Re-install `pip install cli-pipeline==...`


## Paths
* `--model-path` needs to be relative
* On Windows, be sure to use the forward slash `\` for your paths.

## Http/Https Proxy
* Add `--http-proxy=...` and `--https-proxy=...` if you see `CondaHTTPError: HTTP 000 CONNECTION FAILED for url`
* If you see `CondaHTTPError: HTTP 000 CONNECTION FAILED for url` or `[Errno 111] Connection refused'` or `ConnectionError(MaxRetryError("HTTPSConnectionPool`, you need to update `./tensorflow/census/model/pipeline_condarc` to include proxy servers per [THIS](https://conda.io/docs/user-guide/configuration/use-condarc.html#configure-conda-for-use-behind-a-proxy-server-proxy-servers) document.
* For `pip` installs, you may also need to `export HTTP_PROXY` and `export HTTPS_PROXY` within `./tensorflow/census/model/pipeline_setup.sh`
* You may also need to set the lower-case version, as well:  `export http_proxy` and `export https_proxy`
* And if your proxy server password uses special characters (ie. `@`, you may need to convert the characters to [ASCII](https://www.ascii-code.com/) (ie. `%40`).
* You may need to remove the `!#/bin/bash`
* Lastly, you may need to set shell-wide (`~/.bashrc`) and re-source (`. ~/.bashrc`) - or set them as system-wide environment variables (` `) per [THIS](https://help.ubuntu.com/community/EnvironmentVariables#System-wide_environment_variables) document.

## Fixing Docker No Space Left on Device Error
http://phutchins.com/blog/2017/01/04/fixing-docker-no-space-left-on-device/

## PipelineAI 24x7 Support
* Slack:  [![PipelineAI Slack](http://pipeline.ai/assets/img/slack.png)](https://joinslack.pipeline.ai)
* Email:  help@pipeline.ai
* Web:  https://support.pipeline.ai
* Troubleshooting:  [Guide](/docs/troubleshooting)
