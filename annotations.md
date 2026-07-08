Hardware sizing for the software Godot Engine

---

# System requirements

## Desktop or laptop PC - Recommended

| Component | Requirements |
|---|---|
| CPU | • **Windows:** x86_64 CPU with SSE4.2 support, with 4 physical cores or more, ARMv8 CPU<br>  ◦ *Example:* Intel Core i5-6600K, AMD Ryzen 5 1600, Snapdragon X Elite<br><br>• **macOS:** x86_64 or ARM CPU (Apple Silicon)<br>  ◦ *Example:* Intel Core i5-8500, Apple M1<br><br>• **Linux:** x86_64 CPU with SSE4.2 support, ARMv7 or ARMv8 CPU<br>  ◦ *Example:* Intel Core i5-6600K, AMD Ryzen 5 1600, Raspberry Pi 5 with overclocking |
| GPU | • **Forward renderer:** Dedicated graphics with full Vulkan 1.2 support<br>  ◦ *Example:* NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)<br><br>• **Mobile renderer:** Dedicated graphics with full Vulkan 1.2 support<br>  ◦ *Example:* NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)<br><br>• **Compatibility renderer:** Dedicated graphics with full OpenGL 4.6 support<br>  ◦ *Example:* NVIDIA GeForce GTX 650 (Kepler), AMD Radeon HD 7750 (GCN 1.0) |
| RAM | • **Native editor:** 8 GB<br>• **Web editor:** 12 GB |
| Storage | 1.5 GB (used for the executable, project files, all export templates and cache) |
| Operating system | • **Native editor:** Windows 10, macOS 10.15, Linux distribution released after 2020<br>• **Web editor:** Latest version of Firefox, Chrome, Edge, Safari, Opera |

Source: https://docs.godotengine.org/en/stable/about/system_requirements.html

## Comparison

### CPU

Limitation: the teacher said we can't select any processor before 2021

i5-11600K vs Ryzen 5 5600

Ryzen 5 5600 ouperforms by 10.4% and the consumption is lower (65 Watts vs 125 Watts).

The Ryzen 5 5600 provides larger cache capacity than the Core i5-11600K, with twice the L2 cache per core (512 KB vs 256 KB) and a significantly larger L3 cache (32 MB vs 12 MB). Larger caches can reduce the frequency of accesses to slower main memory, improving performance in workloads that repeatedly use the same data.

The Ryzen 5 5600 is manufactured using a 7 nm process, while the Intel Core i5-11600K uses a 14 nm process. A smaller manufacturing process allows more transistors to be placed in the same area, improving energy efficiency and reducing heat generation. This contributes to the Ryzen 5 5600's lower power consumption (65 W TDP compared with 125 W for the i5-11600K), making it easier to cool and more suitable for a workstation that may run development workloads for extended periods.

Ryzen 5 has greater power efficiency.

Source: https://technical.city/en/cpu/Core-i5-11600K-vs-Ryzen-5-5600

Prices: 

- AMD Ryzen 5 5600: BRL 974.66 on Amazon BR
  Source: https://www.amazon.com.br/s?k=AMD+Ryzen+5+5600
- Intel Core i5-11600K: BRL 1.944.27 on Amazon BR
  Source: https://www.amazon.com.br/s?k=Intel+Core+i5-11600k&ref=nb_sb_noss_2

Chosen: Ryzen 5 5600

Reason: According to Technical City's aggregate benchmark, the Ryzen 5 5600 scores approximately 10% higher overall than the Intel Core i5-11600K. It is also cheaper: approximately BRL 975 versus BRL 1,944 (prices may vary depending on the retailer and date).

### Motherboard

Since the selected processor is the AMD Ryzen 5 5600, an AM4 motherboard is required.

Source: https://technical.city/en/cpu/Core-i5-11600K-vs-Ryzen-5-5600 (Socket AM4).

Both B550 and PRO 565 has PCIe 4.0 compatibility among those compatible with AM4, but only B550 has suppport to overclocking, is widely available and has more variety.

Source: https://www.amd.com/en/products/processors/chipsets/am4.html

Chosen chipset: B550

Chosen motherboard: Gigabyte B550M AORUS ELITE - nice price among options (socket AM4 and chipset B550).

### Memory

The godotengine websites recommended 8GB for the Native editor, and 12 GB to the web editor. Since i can have 16 GB in dual channel easyly with 2 8 GB memories, ii prefer to use 16GB in dual channel.

Chosen: KINGSTON FURY BEAST DIMM DDR4 8 GB 3200 MHZ

Reason: Nice price among options.

### 

