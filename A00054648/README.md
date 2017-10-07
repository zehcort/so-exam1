# Exam 1

**Nombre:** Luis Alejandro Tróchez  

**Código:** A00054648


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
