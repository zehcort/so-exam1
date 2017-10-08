# Exam 1

**Nombre:** Luis Alejandro Tróchez  

**Código:** A00054648

**Enlace repositorio:** https://github.com/zehcort/so-exam1


## Desarrollo

## 3.


A continuación, se presentan capturas de pantalla mostrando los comandos usados y su resultado para algunos de los retos presentados en la página https://cmdchallenge.com


•	sum_all_numbers

![][1]

•	replace_spaces_in_filenames

![][2]

•	reverse_readme

![][3]

•	remove_duplicated_lines

![][4]

•	disp_table

![][5]


## 4. 

 
A continuación, se presenta la evidencia de construcción de un script a través del cual se descarga y sobrescribe un libro del proyecto Gutenberg (https://www.gutenberg.org/) a un directorio local cada 5 minutos.
En la siguiente captura, se muestra el directorio en el que se realiza el script y guarda el libro descargado.

![][6]

En el mismo sentido, la siguiente captura muestra el script escrito en bash. En este se hace uso del comando wget con la concatenación de los parámetros que necesita, dado que es necesaria la generación de un número aleatorio para no descargar siempre el mismo. El rango usado para el número del libro fue acortado por motivos de oportunidad de fallo.

![][7]

Por otra parte, para la programación de la ejecución del script cada 5 minutos se hace uso crontab, editando e incluyendo en una línea 6 parámetros en su respectivo orden: que sea cada 5 minutos, que se ejecute todas las horas, todos los días (del 1 al 31), todos los meses, todos los días (de lunes a domingo) y que lo que se ejecute sea script.sh.  Todo esto se muestra a continuación:


![][8]

Por último, para la demostración del funcionamiento se tomaron dos capturas donde se puede ver la hora. En la primera se pueden observar las primeras líneas del archivo de texto donde se guarda el libro (book.txt)

![][9]

## 5.

El objetivo del conocido rickroll es jugar una broma en la que cada vez que el usuario intente reproducir un archivo MP3 se reproduzca uno definido por defecto. Para lograr este cometido, se explicarán 3 procesos a nivel de modificaciones en el kernel: la edición de los llamados al sistema, la creación de un método para poner la ruta del MP3 en lugar de la del archivo que está intentándose abrir y un proceso de restablecimiento del kernel (o CleanUp) antes de cerrar el sistema.
Para el primer proceso, primeramente, se incluyen los módulos necesarios para realizar las llamadas al sistema durante todo el código (módulos, kernel, SysCalls y variables de otros tipos). Luego de esto, se crean los módulos que para ser editados y con ello poder asignar los permisos y definir los tipos de archivos a editar, tales como las siguientes:
•	rickroll_filename: ruta donde se encuentra el archivo a reproducir cuando se abra un MP3.
•	asmlinkage: Variable para llamadas al sistema (SysCalls)
•	 rickroll_open: método para abrir el reproductor de audio del sistema
•	original_sys_open: se utiliza para abrir cualquier tipo de archivo en el PC
•	sys_call_table: variable para manejar la tabla de llamados al sistema

Para cada vez que se abre un archivo, el sistema busca la llamada al sistema para abrir el archivo (en este caso sys_open) y sigue con los otros llamados. En este punto es donde buscamos editar. Se debe verificar que el archivo sea válido (un rickroll_filename verificado) para no provocar un error en el kernel. A continuación, el método busca la tabla de llamados al sistema con ayuda de un método creado por nosotros. Se almacena la tabla obtenida en la variable ya creada para ello. Se verifica que sea válida para poder dirigir el puntero al lugar correcto.
Posterior a esto, se hace uso de las variables de DISABLE_WRITE_PROTECTION y ENABLE_WRITE_PROTECTION con el objetivo de modificar un registro llamado cr0, el cual se encarga de proteger contra la escritura bloques de memoria como los de las llamadas al sistema.

Una vez deshabilitada la protección de escritura se coge de la tabla de llamadas al sistema y se modifica el llamado al sistema encargado de abrir los archivos, llamado NR_open . Se almacena en la variable creada al principio llamada original_sys_open con el objetivo de almacenar el método original en caso de querer volver a él y deshacer la broma
Por último, en este proceso el puntero de la tabla, es decir, este valor de la tabla, debemos apuntarlo hacia nuestro método rickroll_open que será mostrado más en breve y se habilita nuevamente la protección contra escritura.

En segundo lugar, se explica el método rickroll_open, encargado de reemplazar la ruta. Para comenzar, se revisa si el archivo que se está abriendo tiene extensión mp3, ya que es el objeto de la broma. Si no tiene esta extensión el archivo, se abrirá con el llamado al sistema original, almacenado en el original_sys_open. En caso de ser un MP3, utiliza el mismo método original, pero con un cambio en los parámetros, abriendo el archivo almacenado en rickroll_filename.
Como último proceso a explicar, se define un método para el cierre del sistema, el cual busca retornar la estabilidad al sistema antes de salir. Para ello primero se desactiva de nuevo la protección de escritura para poder modificar la tabla y el puntero de abrir archivos lo vuelve a direccionar al método original para abrir archivos. Se activa finalmente la protección de nuevo.


[1]: sum_all_numbers.PNG
[2]: replace_spaces_in_filenames.PNG
[3]: reverse_readme.PNG
[4]: remove_duplicated_lines.PNG
[5]: disp_table.PNG
[6]: IsInMyBooks.PNG
[7]: script.PNG
[8]: crontab.PNG
[9]: 1-book.PNG
[10]: 2-book.PNG
