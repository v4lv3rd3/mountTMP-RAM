# mountTMP-RAM
<li><a name="an_n2"></a><span class="nivel1">Modificaciones a realizar</span> <a href="#an_indice" target="_self" rel="noopener noreferrer">(Volver al índice General)</a><br>
Para realizar esta modificación tendremos que editar el archivo <span class="codigo">/etc/fstab</span>.<p></p>
<blockquote><p><span class="cita"><strong>NOTA:</strong> Es aconsejable hacer una copia de seguridad del archivo <span class="codigo">/etc/fstab</span>. Para hacerlo podemos utilizar el siguiente comando:</span></p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">$ </span><span style="color: #c20cb9; font-weight: bold;">sudo</span> <span style="color: #c20cb9; font-weight: bold;">cp</span> <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>fstab <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>fstab.bak</pre></td></tr></tbody></table><p class="theCode" style="display:none;">$ sudo cp /etc/fstab /etc/fstab.bak</p></div>

<p><span class="cita">Si algo va mal, tan solo tendremos que borrar el archivo <span class="codigo">/etc/fstab</span> modificado con el siguiente comando:</span></p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">$ </span><span style="color: #c20cb9; font-weight: bold;">sudo</span> <span style="color: #c20cb9; font-weight: bold;">rm</span> <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>fstab</pre></td></tr></tbody></table><p class="theCode" style="display:none;">$ sudo rm /etc/fstab</p></div>

<p><span class="cita">y renombrar <span class="codigo">/etc/fstab.bak</span> con el siguiente comando:</span></p>

<div class="wp_syntax" style="position:relative;"><table><tbody><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">$ </span><span style="color: #c20cb9; font-weight: bold;">sudo</span> <span style="color: #c20cb9; font-weight: bold;">mv</span> <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>fstab.bak <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>fstab</pre></td></tr></tbody></table><p class="theCode" style="display:none;">$ sudo mv /etc/fstab.bak /etc/fstab</p></div>

<p></p></blockquote>
<p>Para editar el archivo <span class="codigo">/etc/fstab</span> podemos utilizar el siguiente comando:</p>

<div class="wp_syntax" style="position:relative;"><table><tbody><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">$ </span><span style="color: #c20cb9; font-weight: bold;">sudo</span> <span style="color: #c20cb9; font-weight: bold;">nano</span> <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>fstab</pre></td></tr></tbody></table><p class="theCode" style="display:none;">$ sudo nano /etc/fstab</p></div>

<p>Mostraremos dos métodos prácticamente iguales para el montaje de dichas carpetas en <strong><a href="https://es.wikipedia.org/wiki/Memoria_de_acceso_aleatorio" rel="noopener noreferrer" target="_blank">RAM</a></strong>. Hemos optado por utilizar las opciones de montaje óptimas para unidades <strong><a href="https://es.wikipedia.org/wiki/Unidad_de_estado_s%C3%B3lido" rel="noopener noreferrer" target="_blank">SSD</a></strong>:</p>
<ol>
<li><strong>Primer método:</strong> Añadir al final del archivo <span class="codigo">/etc/fstab</span> las siguiente líneas:

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="text" style="font-family:monospace;">tmpfs /tmp     tmpfs noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</pre></td></tr></tbody></table><p class="theCode" style="display:none;">tmpfs /tmp     tmpfs noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</p></div>


<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="text" style="font-family:monospace;">tmpfs /var/tmp tmpfs noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</pre></td></tr></tbody></table><p class="theCode" style="display:none;">tmpfs /var/tmp tmpfs noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</p></div>

</li>
<li><strong>Segundo método:</strong> Simplemente consiste en hacer un enlace simbólico de <span class="codigo">/var/tmp</span> a <span class="codigo">/tmp</span> y luego solo tendríamos que montar una única carpeta. Los comandos a ejecutar son los siguientes:
<p>Nos situamos en la carpeta <span class="codigo">/var</span>:</p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">$ </span><span style="color: #7a0874; font-weight: bold;">cd</span> <span style="color: #000000; font-weight: bold;">/</span>var</pre></td></tr></tbody></table><p class="theCode" style="display:none;">$ cd /var</p></div>

<p>Una vez allí, eliminamos la carpeta <span class="codigo">/var/tmp</span>:</p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">$ </span><span style="color: #c20cb9; font-weight: bold;">sudo</span> <span style="color: #c20cb9; font-weight: bold;">rm</span> <span style="color: #660033;">-rf</span> <span style="color: #000000; font-weight: bold;">/</span>var<span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span></pre></td></tr></tbody></table><p class="theCode" style="display:none;">$ sudo rm -rf /var/tmp/</p></div>

<p>A continuación, creamos el <strong><a href="https://es.wikipedia.org/wiki/Enlace_simb%C3%B3lico" rel="noopener noreferrer" target="_blank">enlace simbólico</a></strong>:</p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">$ </span><span style="color: #c20cb9; font-weight: bold;">sudo</span> <span style="color: #c20cb9; font-weight: bold;">ln</span> <span style="color: #660033;">-s</span> <span style="color: #000000; font-weight: bold;">/</span>tmp <span style="color: #000000; font-weight: bold;">/</span>var<span style="color: #000000; font-weight: bold;">/</span>tmp</pre></td></tr></tbody></table><p class="theCode" style="display:none;">$ sudo ln -s /tmp /var/tmp</p></div>

<p>y finalmente, añadimos la línea al archivo <span class="codigo">/etc/fstab</span>:</p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="text" style="font-family:monospace;">tmpfs /tmp     tmpfs noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</pre></td></tr></tbody></table><p class="theCode" style="display:none;">tmpfs /tmp     tmpfs noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</p></div>

</li>
<blockquote><p><span class="cita"><strong>NOTA:</strong> Si ya teníamos montadas dichas carpetas, entonces tendremos que, o bien comentar las líneas ya existentes en el archivo <span class="codigo">/etc/fstab</span> y añadir las líneas mostradas anteriormente, o sustituirlas por las que hemos mostrado anteriormente. De lo contrario tendríamos montadas las carpetas en dos ubicaciones distintas a la vez y tendríamos problemas.</span></p></blockquote>
</ol>
<p>Si nuestro sistema utiliza mucha <strong><a href="https://es.wikipedia.org/wiki/Memoria_de_acceso_aleatorio" rel="noopener noreferrer" target="_blank">RAM</a></strong>, por ejemplo, por que utilizamos <strong><a href="https://www.zeppelinux.es/conceptos-basicos-sobre-maquinas-virtuales/" rel="noopener noreferrer" target="_blank">máquinas virtuales</a></strong>, podremos limitar el uso de la <strong><a href="https://es.wikipedia.org/wiki/Memoria_de_acceso_aleatorio" rel="noopener noreferrer" target="_blank">RAM</a></strong> añadiendo el parámetro delimitador <span class="codigo">size</span>. Con este parámetro estamos ordenando al sistema, que bajo ningún concepto conceda más <strong><a href="https://es.wikipedia.org/wiki/Memoria_de_acceso_aleatorio" rel="noopener noreferrer" target="_blank">RAM</a></strong> a dichos puntos de montaje que el indicado con el parámetro <span class="codigo">size</span>. A continuación ponemos un ejemplo de como limitar el tamaño asignado a <strong>2GB</strong>:</p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="text" style="font-family:monospace;">tmpfs /tmp     tmpfs size=2G,noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</pre></td></tr></tbody></table><p class="theCode" style="display:none;">tmpfs /tmp     tmpfs size=2G,noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</p></div>

</li>
