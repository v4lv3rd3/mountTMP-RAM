#mountTMP-RAM
<li><a name="an_n2"></a><span class="nivel1">Modificaciones a realizar</span>
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

<p>Mostraremos dos métodos prácticamente iguales para el montaje de dichas carpetas en <strong>RAM</strong>. Hemos optado por utilizar las opciones de montaje óptimas para unidades <strong>SSD</strong>:</p>
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

<p>A continuación, creamos el <strong>enlace simbólico</strong>:</p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">$ </span><span style="color: #c20cb9; font-weight: bold;">sudo</span> <span style="color: #c20cb9; font-weight: bold;">ln</span> <span style="color: #660033;">-s</span> <span style="color: #000000; font-weight: bold;">/</span>tmp <span style="color: #000000; font-weight: bold;">/</span>var<span style="color: #000000; font-weight: bold;">/</span>tmp</pre></td></tr></tbody></table><p class="theCode" style="display:none;">$ sudo ln -s /tmp /var/tmp</p></div>

<p>y finalmente, añadimos la línea al archivo <span class="codigo">/etc/fstab</span>:</p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="text" style="font-family:monospace;">tmpfs /tmp     tmpfs noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</pre></td></tr></tbody></table><p class="theCode" style="display:none;">tmpfs /tmp     tmpfs noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</p></div>

</li>
<blockquote><p><span class="cita"><strong>NOTA:</strong> Si ya teníamos montadas dichas carpetas, entonces tendremos que, o bien comentar las líneas ya existentes en el archivo <span class="codigo">/etc/fstab</span> y añadir las líneas mostradas anteriormente, o sustituirlas por las que hemos mostrado anteriormente. De lo contrario tendríamos montadas las carpetas en dos ubicaciones distintas a la vez y tendríamos problemas.</span></p></blockquote>
</ol>
<p>Si nuestro sistema utiliza mucha <strong>RAM</strong>, por ejemplo, por que utilizamos <strong>máquinas virtuales</strong>, podremos limitar el uso de la <strong>RAM</strong> añadiendo el parámetro delimitador <span class="codigo">size</span>. Con este parámetro estamos ordenando al sistema, que bajo ningún concepto conceda más <strong>RAM</strong> a dichos puntos de montaje que el indicado con el parámetro <span class="codigo">size</span>. A continuación ponemos un ejemplo de como limitar el tamaño asignado a <strong>2GB</strong>:</p>

<div class="wp_syntax" style="position: relative; width: auto;"><table><tbody><tr><td class="code"><pre class="text" style="font-family:monospace;">tmpfs /tmp     tmpfs size=2G,noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</pre></td></tr></tbody></table><p class="theCode" style="display:none;">tmpfs /tmp     tmpfs size=2G,noexec,rw,auto,nouser,sync,noatime,nodev,nosuid,mode=1777 0 0</p></div>

</li>

<ul>
<li><strong>noatime:</strong> Deshabilita por completo el registro de tiempo de acceso para cualquier archivo. Implica la aplicación de <span class="codigo">nodiratime</span>. Teniendo en cuanta que además se anota el acceso a los ficheros cacheados y el acceso constante a todos los ficheros de procesos del sistema, es un número muy importante de escrituras de fechas de acceso. <strong><em>Al reducir la cantidad de escrituras que el sistema operativo realiza sobre el disco, incrementamos la vida de la unidad SSD</em></strong>.</li>
<li><strong>nodiratime:</strong> Deshabilita el registro de tiempos de acceso para los directorios, pero mantiene activo el registro para los archivos.</li>
<li><strong>relatime:</strong> Limita el registro de <strong>timestamps</strong> únicamente a aquellos casos en que el archivo se modifica.</li>
<blockquote><p><span class="cita">De las tres opciones anteriores, la opción menos invasiva es claramente <span class="codigo">relatime</span>, que ya de por sí ofrecerá alguna ganancia en el rendimiento de nuestros discos duros, sobre todo mecánicos. La opción que más rendimiento ofrece es <span class="codigo">noatime</span>.</span></p></blockquote>
<li><strong>size:</strong> Opción válida solo para sistemas <strong>tmpfs</strong>. Limita el tamaño que se utilizará de RAM. Por defecto se utiliza como máximo la mitad de la memoria RAM. También se puede expresar el tamaño en porcentajes de memoria RAM. Por ejemplo <code>size=50%</code>.</li>
<li><strong>defaults:</strong> Asigna las opciones de montaje predeterminadas que serán utilizadas para el sistema de archivos. Las opciones predeterminadas para ext4 son: rw, suid, dev, exec, auto, nouser, async.</li>
<li><strong>rw:</strong> Monta el sistema de archivos en modo lectura-escritura.</li>
<li><strong>ro:</strong> Monta el sistema de archivos en modo sólo lectura.</li>
<li><strong>suid:</strong> Permite las operaciones de suid, y sgid bits. Se utiliza principalmente para permitir a los usuarios comunes ejecutar binarios con privilegios concedidos temporalmente con el fin de realizar una tarea específica.</li>
<li><strong>nosuid:</strong> Bloquea el funcionamiento de suid, y sgid bits.</li>
<li><strong>exec:</strong> Permite la ejecución de binarios residentes en el sistema de archivos.</li>
<li><strong>noexec:</strong> No permite la ejecución de binarios que se encuentren en el sistema de archivos.</li>
<li><strong>auto:</strong> El sistema de archivos será montado automáticamente durante el arranque, o cuando la orden mount -a se invoque.</li>
<li><strong>noauto:</strong> El sistema de archivos no será montado automáticamente, solo cuando se le ordene manualmente.</li>
<li><strong>user:</strong> Permite a cualquier usuario montar el sistema de archivos. Esta opción incluye noexec, nosuid, nodev, a menos que se indique lo contrario.</li>
<li><strong>nouser:</strong> Solo el usuario root puede montar el sistema de archivos.</li>
<li><strong>users:</strong> Permite que cualquier usuario perteneciente al grupo users montar el sistema de archivos.</li>
<li><strong>owner:</strong> Permite al propietario del dispositivo montarlo.</li>
<li><strong>dev:</strong> Intérprete de los dispositivos especiales o de bloque del sistema de archivos.</li>
<li><strong>nodev:</strong> Impide la interpretación de los dispositivos especiales o de bloques del sistema de archivos.</li>
<li><strong>sync:</strong> Todo el I/O se debe hacer de forma sincrónica.</li>
<li><strong>async:</strong> Todo el I/O se debe hacer de forma asíncrona.</li>
<li><strong>discard:</strong> Emite las órdenes TRIM para dispositivos de bloques subyacentes cuando se liberan los bloques. Recomendado para usar si el sistema de archivos se encuentra en un <strong>sistema de ficheros</strong> ubicados en unidades <strong>SSD</strong>.</li>
<li><strong>nodelalloc:</strong> Desactiva la función de <strong>ext4</strong> de <strong>delayed allocation</strong>, que reserva el espacio pero no lo escribe. Aplaza la escritura de bloques hasta que se esté en el tiempo de escritura. Es más que nada por seguridad.</li>
<li><strong>barrier=0:</strong>  Desactiva las barreras automáticamente. Se refiere a los límites de escritura. Si es <strong>igual a cero los elimina</strong>, si es <strong>igual a 1, los activa</strong>. Podemos prescindir de estas barreras si los discos están protegidos contra cortes de corriente. Sólo en este caso, incluimos la opción <span class="codigo">barrier=0</span></li>
<li><strong>i_version:</strong> Habilita el uso de la versión extendida de 64 bits en sistemas de ficheros <strong>ext4</a></strong>.</li>
<li><strong>commit=30:</strong> Retrasa la escritura de los metadatos de ficheros, con lo que se reduce mucho el uso de disco. No recomendable si estuviésemos en un ordenador con batería.</li>
<li><strong>inode_readahead_blks=64:</strong> Aumenta de <strong>32</strong> a <strong>64</strong> el tamaño de los bloques de lectura.</li>
<li><strong>data=writeback:</strong> Evita que los metadatos de los archivos sean escritos de forma lenta tras escribir los archivos. Esta opción no provoca corrupción en el sistema de archivos, pero puede provocar que los cambios mas recientes se pierdan si cae el sistema. <span style="color:red;">No lo incluiremos en nuestros ejemplos ya que no funciona en algunos sistemas</span>.</li>
<li><strong>flush:</strong> La opción <strong>vfat</strong> permite eliminar datos con más frecuencia, de modo que los cuadros de diálogo de copia o las barras de progreso se mantenga hasta que se hayan escrito todos los datos.</li>
<li><strong>nofail:</strong> Monta el dispositivo cuando está presente, pero ignora su ausencia. Esto evita que se cometan errores durante el arranque para los medios extraíbles.</li>
<li><strong>mode=1777:</strong> Permite que cualquiera pueda crear archivos, pero protegiéndolos de la manipulación de otros usuarios.</li>
</ul>
