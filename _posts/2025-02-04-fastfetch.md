---
title: How to Install Fastfetch on Ubuntu
categories: [linux, ubuntu, homelab, terminal, productivity]
tags: [linux, ubuntu, homelab, terminal, productivity]
---

I've been seeing a lot of hype around tools like **neofetch** and **fastfetch** so I decided to
give one a try.

With tools like neofetch and fastfetch you can see a quick overview of essential system details like CPU, GPU, RAM usage, and OS version, all displayed in a sleek and visually appealing format. 
I decided to go with Fastfetch since it's a faster, more efficient alternative to Neofetch, offering better performance and greater customization options. 
Plus, neofetch is no longer being maintained.

> Ubuntu 22.04, 24.04 and 24.10 you can use an unofficial (but officially endorsed) [Fastfetch PPA](https://launchpad.net/~zhangsongcui3371/+archive/ubuntu/fastfetch) to get the latest, or download the DEB installer from the project’s [Github releases page](https://github.com/fastfetch-cli/fastfetch/releases/tag/2.35.0)

---

## Installing Fastfetch on Ubuntu

Fastfetch is available in Ubuntu’s repositories, for versions of Ubuntu 24.10 and new, making installing it simple:

```bash
sudo apt install fastfetch
```

For 


---

## Running Fastfetch

Once installed, you can run Fastfetch by simply typing:

```bash
fastfetch
```

This will display system information along with your distribution’s ASCII logo.

## Customizing Fastfetch

One of the best features of Fastfetch is its customization. You can tweak the output by modifying its configuration file.

To generate a default configuration file, run:

```bash
fastfetch --gen-config
```

This will create a configuration file in:

```bash
~/.config/fastfetch/config.jsonc
```

You can edit this file using any text editor:

```bash
nano ~/.config/fastfetch/config.jsonc
```

From here, you can modify what system details are displayed, change colors, and even adjust the ASCII logo style.

## Example Customization

If you want a minimal output that only displays your OS, CPU, and RAM usage, you can modify the `config.jsonc` file like this:

```json
{
  "modules": [
    { "type": "OS" },
    { "type": "CPU" },
    { "type": "Memory" }
  ]
}
```

Save the file and run:

```bash
fastfetch
```

Your output will now only show the selected information.

---

## Conclusion

Fastfetch is a fantastic tool for adding both aesthetics and functionality to your terminal. Whether you just want a cool-looking system info display or a completely tailored experience, it provides the flexibility to suit your needs.

Now, every time you open your terminal, you'll get a sleek, informative snapshot of your system in style!

