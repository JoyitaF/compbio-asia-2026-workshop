# 1. Computing Environment and Cyberinfrastructure

**Source:** `0615-02-CompBioAsia2025_compute_environment.pptx`  
**Date indicated by filename:** 15 June 2026  
**Instructor / credit shown:** Travis Wheeler; material also credited to Michele Cosi.

The computing-environment session explained the basic workshop infrastructure: instead of requiring every participant to install complicated scientific software locally, the workshop provided remote machines with software already installed. Participants only needed to log in and work in the provided environment.

The practical teaching was not just “use the server.” It introduced the difference between local laptops, remote virtual machines, HPC/supercomputer resources, CPUs, GPUs, and persistent storage. A key lesson was that computation in biology is often limited by environment management before it is limited by algorithms. If Python packages, GPU drivers, molecular simulation packages, or database paths are broken, the science cannot even start.

Important practical ideas:

- **SSH:** a secure way to log into a remote machine from your own computer.
- **Persistent storage:** a directory that keeps your files even if the temporary compute environment disappears.
- **Ephemeral systems:** compute sessions that may reset; files stored only there can vanish.
- **Symlink:** a symbolic link is like a shortcut or alias from one filesystem location to another. The workshop example used a command like `ln -s /data/user_dirs/[your_name] ~/my_files`, which creates `~/my_files` as a convenient pointer to a persistent directory.
- **Jupyter/CACAO-style managed environments:** participants could open notebooks without manually installing every dependency.

This mattered later because molecular dynamics and AlphaFold workflows produce many large files, and a small path mistake can break a pipeline. The same logic applies to cluster work: keep raw inputs, outputs, scripts, and analysis results in durable locations.

See also: [`lectures/01-computing-environment.md`](lectures/01-computing-environment.md)
