Actores:
    Empleado de mesa de entradas.
    Empleado de rendiciones.
    Servidor de la AFIP

Casos de uso:
    Confeccionar minuta.
    Aprobar minuta.
    Verificacion AFIP.
    Imprimir listados.

--------------------------------------------------------------------------

Nombre del caso de uso: confeccionar minuta.
Descripcion: este caso de uso describe el evento en el empleado de mesa de entradas confecciona una minuta.

Actores: empleado de mesa de entradas.

Precondiciones: 

Curso normal: 
    Accion del Actor: 
        Paso 1: el empleado de mesa de entradas presiona "Confeccionar minuta".
        Paso 3: el empleado ingresa los datos solicitados.

    Accion del sistema: 
        Paso 2: el sistema le solicita que ingrese nombre y número de CUIT de la persona a contratar, tipo de contrato, fecha de comienzo, duración y monto.
        Paso 4: el sistema valida los datos ingresados.
        Paso 5: el sistema le asocia un numero de minuta e informa que se confecciono con exito la minuta.

Curso alterno:
    Paso 4: el sistema detecta que el monto ingresado supera los $25.000 e informa el error en pantalla. Vuelve al paso 2.
    Paso 4: el sistema detecta que la duracion del contrato supera los 6 meses e informa el error en pantalla. Vuelve al paso 2.

Post condicion: se realiza la minuta, se le asigna un numero y queda pendiente de aprobacion.

--------------------------------------------------------------------------

Nombre de caso: aprobar minuta.
Descripcion: este caso de uso describe el evento en el que un empleado de rendiciones aprueba una minuta.

Actores: empleado de rendiciones.

Precondiciones:

Curso normal:
    Accion del actor:
        Paso 1: el empleado de rendiciones presiona "Aprobar minuta".
        Paso 3: el empleado ingresa los datos solicitados.
    Accion del sistema:
        Paso 2: el sistema le solicita que ingrese el numero de minuta.
        Paso 4: el sistema verifica los datos ingresados.
        Paso 5: el sistema muestra en pantalla los datos de la minutas.
        Paso 6: el sistema verifica si la persona a contratar tiene 3 contratos vigentes.
        Paso 7: se ejecuta el caso de uso "Verificar AFIP".
        Paso 8: el sistema recibe el resultado de la verificacion AFIP.
        Paso 9: se aprueba la minuta.

Curso alterno:
    Paso 4: el sistema informa que ese numero de minuta es inexistente. Vuelve al paso 2.
    Paso 6: el sistema informa que la persona a contratar tiene 3 contratos vigentes.
    Paso 7: fallo la ejecucion del caso de uso "Verficar AFIP".
    Paso 9: el sistema informa que el CUIT de la persona a contratar esta inhabilitada por AFIP.

Postcondicion: se aprobo la minuta.

--------------------------------------------------------------------------

Nombre de caso: verificar AFIP.
Descripcion: este caso de uso describe el evento en el que el servidor de la AFIP
verifica si el CUIT de la persona esta habilitado o no.

Actores: servidor de la AFIP.

Precondiciones: 

Curso normal:
    Accion del actor:
        Paso 3: la AFIP verifica que el token sea uno valido.
        Paso 4: la AFIP analiza el CUIT de la persona a contratar.
        Paso 5: la AFIP le envia la respuesta al sistema.
        
    Accion del sistema:
        Paso 1: el sistema se conecta con el servidor AFIP.
        Paso 2: el sistema le envia el token a la AFIP.
        Paso 6: el sistema recibe la respuesta de la AFIP.

Curso alterno:
    Paso 1: la conexion con el servidor de la AFIP no se puede realizar, informa del error ocurrido.
    Paso 3: la AFIP le informa al sistema que el token ingresado no es valido.

Postcondicion: se verifica el CUIT de la persona a contratar.

--------------------------------------------------------------------------

Nombre de caso: imprimir listados.
Descripcion: este caso de uso describe el evento en el que el empleado de rendiciones imprime el listado con las minutas aprobadas.

Actores: empleado de rendiciones.

Precondiciones: 

Curso normal:
    Accion del actor:
        Paso 1: el empleado de rendiciones presiona "Imprimir listado".
        
    Accion del sistema:
        Paso 2: el sistema imprime el listado de minutas aprobadas.        

Curso alterno:
    Paso 2: el sistema informa que el listado de minutas aprobadas esta vacio. Fin de CU.

Postcondiciones: se imprime el listado de minutas aprobadas.