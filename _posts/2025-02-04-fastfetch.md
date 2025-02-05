---
title: How to Install Fastfetch on Ubuntu
categories: [linux, ubuntu, homelab, terminal, productivity]
tags: [linux, ubuntu, homelab, terminal, productivity]
---

Before diving into setting up applications, I wanted to start with a neat and functional terminal setup. Terminal customizations can significantly improve productivity while also making the terminal look much cooler.

One of the first tools I installed is **Fastfetch**, a lightweight and highly customizable system information tool. It provides a quick overview of essential system details like CPU, GPU, RAM usage, and OS version, all displayed in a sleek and visually appealing format. Fastfetch is a faster, more efficient alternative to **Neofetch**, offering better performance and greater customization options. Plus, it features ASCII artwork of your Linux distribution's logo, making your terminal both informative and stylish.

Let’s start by installing Fastfetch.

---

## Installing Fastfetch on Ubuntu

Fastfetch is available in Ubuntu’s repositories, so installing it is simple:

```bash
sudo apt install fastfetch
```

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

