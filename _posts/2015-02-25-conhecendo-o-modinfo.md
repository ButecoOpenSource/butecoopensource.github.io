---
layout: wordpress
title: Conhecendo o modinfo
excerpt: |
  Este artigo explica o funcionamento básico do comando kmod, e para que qual finalidade existe o comando. Ainda neste artigo, é mostrado exemplos de execução do comando e quais informações este pode extrair dos módulos do kernel.
date: 2015-02-25 23:54:31
author: marcossouza
permalink: /conhecendo-o-modinfo/
image: /assets/wp-content/uploads/2015/02/LXF117.fix_.illo_penguin-e1424908179658.jpg
categories:
  - Dicas
tags:
  - kernel
  - linux
  - terminal
---

<p style="text-align: justify;">Enquanto estudava para a prova LPI 101, eu acabei estudando os comandos que tratam de módulos do kernel. Alguns comandos eu já conhecia, como <em>insmod</em> para carregar um módulo do kernel, e <em>rmmod</em> para remover um módulo já carregado. Mas entre estes eu acabei encontrando o <em>modinfo</em>. Este comando busca informações de um módulo do kernel. Todos estes comandos fazem parte do pacote <em>kmod</em>, e este pacote existe em praticamente todas as distribuições Linux.</p>
Segue abaixo a execução do modinfo no driver i915, que é o driver para placas gráficas da Intel.

<pre><code class="bash">
&lt;h5&gt;&lt;em&gt;marcos@xfiles: [~] # modinfo i915&lt;/em&gt;
&lt;em&gt; filename: /lib/modules/3.18.5-201.fc21.x86_64/kernel/drivers/gpu/drm/i915/i915.ko.xz&lt;/em&gt;
&lt;em&gt; license: GPL and additional rights&lt;/em&gt;
&lt;em&gt; description: Intel Graphics&lt;/em&gt;
&lt;em&gt; author: Intel Corporation&lt;/em&gt;
&lt;em&gt; author: Tungsten Graphics, Inc.&lt;/em&gt;
&lt;em&gt; …&lt;/em&gt;
&lt;em&gt; alias: pci:v00008086d00003582sv*sd*bc03sc*i*&lt;/em&gt;
&lt;em&gt; alias: pci:v00008086d00002562sv*sd*bc03sc*i*&lt;/em&gt;
&lt;em&gt; alias: pci:v00008086d00003577sv*sd*bc03sc*i*&lt;/em&gt;
&lt;em&gt; depends: drm_kms_helper,drm,video,i2c-algo-bit&lt;/em&gt;
&lt;em&gt; intree: Y&lt;/em&gt;
&lt;em&gt; vermagic: 3.18.5-201.fc21.x86_64 SMP mod_unload&lt;/em&gt;
&lt;em&gt; signer: Fedora kernel signing key&lt;/em&gt;
&lt;em&gt; sig_key: 3F:8E:A9:86:28:8C:19:99:F3:2A:50:D2:A3:7C:05:E5:4D:E8:EC:1E&lt;/em&gt;
&lt;em&gt; sig_hashalgo: sha256&lt;/em&gt;
&lt;em&gt; parm: modeset:Use kernel modesetting [KMS] (0=DRM_I915_KMS from .config, 1=on, -1=force vga console preference [default]) (int)&lt;/em&gt;
&lt;em&gt; parm: panel_ignore_lid:Override lid status (0=autodetect, 1=autodetect disabled [default], -1=force lid closed, -2=force lid open) (int)&lt;/em&gt;
&lt;em&gt; parm: powersave:Enable powersavings, fbc, downclocking, etc. (default: true) (int)&lt;/em&gt;
&lt;em&gt; parm: semaphores:Use semaphores for inter-ring sync (default: -1 (use per-chip defaults)) (int)&lt;/em&gt;
&lt;em&gt; parm: enable_rc6:Enable power-saving render C-state 6. Different stages can be selected via bitmask values (0 = disable; 1 = enable rc6; 2 = enable deep rc6; 4 = enable deepest rc6). For example, 3 would enable rc6 and deep rc6, and 7 would enable everything. default: -1 (use per-chip default) (int)&lt;/em&gt;
&lt;em&gt; parm: enable_fbc:Enable frame buffer compression for power savings (default: -1 (use per-chip default)) (int)&lt;/em&gt;
&lt;em&gt; parm: lvds_downclock:Use panel (LVDS/eDP) downclocking for power savings (default: false) (int)&lt;/em&gt;
&lt;em&gt; parm: lvds_channel_mode:Specify LVDS channel mode (0=probe BIOS [default], 1=single-channel, 2=dual-channel) (int)&lt;/em&gt;
&lt;em&gt; parm: lvds_use_ssc:Use Spread Spectrum Clock with panels [LVDS/eDP] (default: auto from VBT) (int)&lt;/em&gt;
&lt;em&gt; parm: vbt_sdvo_panel_type:Override/Ignore selection of SDVO panel mode in the VBT (-2=ignore, -1=auto [default], index in VBT BIOS table) (int)&lt;/em&gt;
&lt;em&gt; parm: reset:Attempt GPU resets (default: true) (bool)&lt;/em&gt;
&lt;em&gt; parm: enable_hangcheck:Periodically check GPU activity for detecting hangs. WARNING: Disabling this can cause system wide hangs. (default: true) (bool)&lt;/em&gt;
&lt;em&gt; parm: enable_ppgtt:Override PPGTT usage. (-1=auto [default], 0=disabled, 1=aliasing, 2=full) (int)&lt;/em&gt;
&lt;em&gt; parm: enable_execlists:Override execlists usage. (-1=auto, 0=disabled [default], 1=enabled) (int)&lt;/em&gt;
&lt;em&gt; parm: enable_psr:Enable PSR (default: false) (int)&lt;/em&gt;
&lt;em&gt; parm: preliminary_hw_support:Enable preliminary hardware support. (int)&lt;/em&gt;
&lt;em&gt; parm: disable_power_well:Disable the power well when possible (default: true) (int)&lt;/em&gt;
&lt;em&gt; parm: enable_ips:Enable IPS (default: true) (int)&lt;/em&gt;
&lt;em&gt; parm: fastboot:Try to skip unnecessary mode sets at boot time (default: false) (bool)&lt;/em&gt;
&lt;em&gt; parm: prefault_disable:Disable page prefaulting for pread/pwrite/reloc (default:false). For developers only. (bool)&lt;/em&gt;
&lt;em&gt; parm: invert_brightness:Invert backlight brightness (-1 force normal, 0 machine defaults, 1 force inversion), please report PCI device ID, subsystem vendor and subsystem device ID to dri-devel@lists.freedesktop.org, if your machine needs it. It will then be included in an upcoming module version. (int)&lt;/em&gt;
&lt;em&gt; parm: disable_display:Disable display (default: false) (bool)&lt;/em&gt;
&lt;em&gt; parm: disable_vtd_wa:Disable all VT-d workarounds (default: false) (bool)&lt;/em&gt;
&lt;em&gt; parm: enable_cmd_parser:Enable command parsing (1=enabled [default], 0=disabled) (int)&lt;/em&gt;
&lt;em&gt; parm: use_mmio_flip:use MMIO flips (-1=never, 0=driver discretion [default], 1=always) (int)&lt;/em&gt;
&lt;em&gt; parm: mmio_debug:Enable the MMIO debug code (default: false). This may negatively affect performance. (bool)&lt;/em&gt;
&lt;em&gt; parm: verbose_state_checks:Enable verbose logs (ie. WARN_ON()) in case of unexpected hw state conditions. (bool)&lt;/em&gt;&lt;/h5&gt;
</code></pre>

<p style="text-align: justify;">Além de informações sobre os responsáveis pela criação e manutenção do driver, o <em>modinfo</em> também mostra todos os parâmetros aceitos pelo driver em tempo de boot. Estes parâmetros têm a capacidade de alterar o comportamento do driver.</p>
<p style="text-align: justify;">Vamos a mais um exemplo, agora mostrando a saída do modinfo para o driver nouveau, que é o driver open source para as placas de vídeo da NVIDIA:</p>


<pre><code class="bash">
&lt;h5&gt;&lt;em&gt;marcos@xfiles: [~] # modinfo nouveau&lt;/em&gt;
&lt;em&gt; filename: /lib/modules/3.18.5-201.fc21.x86_64/kernel/drivers/gpu/drm/nouveau/nouveau.ko.xz&lt;/em&gt;
&lt;em&gt; license: GPL and additional rights&lt;/em&gt;
&lt;em&gt; description: nVidia Riva/TNT/GeForce/Quadro/Tesla&lt;/em&gt;
&lt;em&gt; author: Nouveau Project&lt;/em&gt;
&lt;em&gt; alias: pci:v000012D2d*sv*sd*bc03sc*i*&lt;/em&gt;
&lt;em&gt; alias: pci:v000010DEd*sv*sd*bc03sc*i*&lt;/em&gt;
&lt;em&gt; depends: drm,drm_kms_helper,ttm,mxm-wmi,wmi,video,i2c-algo-bit&lt;/em&gt;
&lt;em&gt; intree: Y&lt;/em&gt;
&lt;em&gt; vermagic: 3.18.5-201.fc21.x86_64 SMP mod_unload&lt;/em&gt;
&lt;em&gt; signer: Fedora kernel signing key&lt;/em&gt;
&lt;em&gt; sig_key: 3F:8E:A9:86:28:8C:19:99:F3:2A:50:D2:A3:7C:05:E5:4D:E8:EC:1E&lt;/em&gt;
&lt;em&gt; sig_hashalgo: sha256&lt;/em&gt;
&lt;em&gt; parm: pstate:enable sysfs pstate file, which will be moved in the future (int)&lt;/em&gt;
&lt;em&gt; parm: tv_norm:Default TV norm.&lt;/em&gt;
&lt;em&gt; Supported: PAL, PAL-M, PAL-N, PAL-Nc, NTSC-M, NTSC-J,&lt;/em&gt;
&lt;em&gt; hd480i, hd480p, hd576i, hd576p, hd720p, hd1080i.&lt;/em&gt;
&lt;em&gt; Default: PAL&lt;/em&gt;
&lt;em&gt; *NOTE* Ignored for cards with external TV encoders. (charp)&lt;/em&gt;
&lt;em&gt; parm: tv_disable:Disable TV-out detection (int)&lt;/em&gt;
&lt;em&gt; parm: ignorelid:Ignore ACPI lid status (int)&lt;/em&gt;
&lt;em&gt; parm: duallink:Allow dual-link TMDS (default: enabled) (int)&lt;/em&gt;
&lt;em&gt; parm: nofbaccel:Disable fbcon acceleration (int)&lt;/em&gt;
&lt;em&gt; parm: agpmode:AGP mode (0 to disable AGP) (int)&lt;/em&gt;
&lt;em&gt; parm: vram_pushbuf:Create DMA push buffers in VRAM (int)&lt;/em&gt;
&lt;em&gt; parm: config:option string to pass to driver core (charp)&lt;/em&gt;
&lt;em&gt; parm: debug:debug string to pass to driver core (charp)&lt;/em&gt;
&lt;em&gt; parm: noaccel:disable kernel/abi16 acceleration (int)&lt;/em&gt;
&lt;em&gt; parm: modeset:enable driver (default: auto, 0 = disabled, 1 = enabled, 2 = headless) (int)&lt;/em&gt;
&lt;em&gt; parm: runpm:disable (0), force enable (1), optimus only default (-1) (int)&lt;/em&gt;&lt;/h5&gt;
</code></pre>

<p style="text-align: justify;">Ainda podemos notar pelo campo <em>depends</em>, quais os módulos que dependem do módulo listado, o tipo de licença do módulo, o caminho onde se encontra o módulo dentro do sistema de arquivos e muitas outras informações interessantes para quem tem interesse em device drivers, ou está curioso para saber como estes se organizam.</p>
<p style="text-align: justify;">Espero que tenham gostado. Qualquer dúvida ou sugestão, por favor comente a postagem. Se inscreva em nossos perfis nas redes sociais para saber em primeira mão quando lançamos novos artigos. Até mais!</p>
Referências:
<a title="http://linux.die.net/man/8/modinfo" href="http://linux.die.net/man/8/modinfo" target="_blank">modinfo</a>
<a title="http://linux.die.net/man/8/insmod" href="http://linux.die.net/man/8/insmod" target="_blank">insmod</a>
<a title="http://linux.die.net/man/8/rmmod" href="http://linux.die.net/man/8/rmmod" target="_blank">rmmod</a>
<a title="http://man7.org/linux/man-pages/man8/kmod.8.html" href="http://man7.org/linux/man-pages/man8/kmod.8.html" target="_blank">kmod</a>