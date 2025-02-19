# Update

1.  My fork's name was n_gpu, but I find that if we want to uninstall it , we should use `pip uninstall
gpustat`, so the n_gpu is missing. So switch back to gpustat. 

2.  For better experience for Chinese users, I mainly focus on  https://gitee.com/llwwff/gpustat
    instead of github' s repo

---  

n_gpu: number of available gpu / new gpu command, do not use the ugly nvidia-smi anymore.

# Install

```python -m pip install git+https://github.com/sisrfeng/n_gpu```  

* forked from   wookayin/gpustat  (v0.6)  (The original repo' s version is higher now, but I'm quite satisfied with this version.)  

* The code is not  complex: `gpu_stats` in main.py  call `print_formatted(sys.stdout, **kwargs)` in core.py.  
I just modified the two files above.





# Automatically Find the GPUs with Most MEM Available 

`nvidia-smi` then set `CUDA_VISIBLE_DEVICES` manually?  

I have not typed these two for a long time.

`source alias.zsh`  in your zshrc file, then type `p` in zsh instead of `python3` 

See ./find_gpus.py and alias.zsh before you use them!   

   
      

# Original README.md  


`gpustat`
=========

[![pypi](https://img.shields.io/pypi/v/gpustat.svg?maxAge=86400)][pypi_gpustat]
[![Build Status](https://travis-ci.org/wookayin/gpustat.svg?branch=master)](https://travis-ci.org/wookayin/gpustat)
[![license](https://img.shields.io/github/license/wookayin/gpustat.svg?maxAge=86400)](LICENSE)


![Screenshot: gpustat -cp](screenshot.png)

no AMD support as of now

Usage
-----

`$ gpustat`

Options:

* `--color`            : Force colored output (even when stdout is not a tty)
* `--no-color`         : Suppress colored output
* `-u`, `--show-user`  : Display username of the process owner
* `-c`, `--show-cmd`   : Display the process name
* `-f`, `--show-full-cmd`   : Display full command and cpu stats of running process
* `-p`, `--show-pid`   : Display PID of the process
* `-F`, `--show-fan`   : Display GPU fan speed
* `-e`, `--show-codec` : Display encoder and/or decoder utilization
* `-P`, `--show-power` : Display GPU power usage and/or limit (`draw` or `draw,limit`)
* `-a`, `--show-all`   : Display all gpu properties above
* `--watch`, `-i`, `--interval`   : Run in watch mode (equivalent to `watch gpustat`) if given. Denotes interval between updates. ([#41][gh-issue-41])
* `--json`             : JSON Output (Experimental, [#10][gh-issue-10])

### Tips

- To periodically watch,
    try `gpustat --watch` or `gpustat -i` ([#41][gh-issue-41]).
    - For older versions,
        one may use `watch --color -n1.0 gpustat --color`.
- Running `nvidia-smi daemon` (root privilege required)
    will make the query much **faster** and use less CPU ([#54][gh-issue-54]).
- The GPU ID (index) shown by `gpustat` (and `nvidia-smi`)
  is PCI BUS ID,
      while CUDA differently assigns the fastest GPU with the lowest ID by default.
  Therefore, in order to make CUDA and `gpustat` use **same GPU index**,
    configure the `CUDA_DEVICE_ORDER` environment variable to `PCI_BUS_ID`
    (before setting `CUDA_VISIBLE_DEVICES` for your CUDA program):
        `export CUDA_DEVICE_ORDER=PCI_BUS_ID`.


Starting from v1.0, gpustat will support [only Python 3.4+][gh-issue-66]. 

[pypi_gpustat]: https://pypi.python.org/pypi/gpustat
[gh-issue-10]: https://github.com/wookayin/gpustat/issues/10
[gh-issue-41]: https://github.com/wookayin/gpustat/issues/41
[gh-issue-54]: https://github.com/wookayin/gpustat/issues/54
[gh-issue-66]: https://github.com/wookayin/gpustat/issues/66

Default display
---------------

> [0] GeForce GTX Titan X | 77'C,  96 % | 11848 / 12287 MB | python/52046(11821M)

- `[0]`: GPUindex (starts from 0) as PCI_BUS_ID
- `GeForce GTX Titan X`: GPU name
- `77'C`: Temperature
- `96 %`: Utilization
- `11848 / 12287 MB`: GPU Memory Usage
- `python/...`: Running processes on GPU (and their memory usage)


License
-------

[MIT License](LICENSE)
