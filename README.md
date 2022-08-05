# Prácticas de Seguridad en los servicios de Azure
![securityLogo](/images/securityCenter.png)

## Índice
### [Introducción](#introducción)
### [Prerrequisitos](#prerrequisitos-para-las-prácticas)
### [Práctica con Azure Key Vault](#práctica-azure-key-vault) 
### [Práctica con Grupos de Seguridad de Red](#práctica-nsg)

------

### Introducción

La seguridad es importante tanto en el mundo real, como en el virutal y la nube no se excenta de esto. En Azure, se cuentan con diversos servicios de ciberseguridad para poder proteger y mitigar amenazas de atacantes y mantener a salvo los datos de los clientes que buscan la confidencialidad, integridad y dispobinibilidad de aquellos datos en juego. Algunos de los servicios de seguridad de Azure son:


#### Microsoft Defender for Cloud ![MDC](/images/icon-Azure-Defender.svg)

Este servicio porporciona los niveles de seguridad de los servicios en la nube, además de ofrecer recomendaciones de seguridad y puede aplicar de forma automática configuraciones específicas que se requieran. Es un servicio tipo [SaaS](https://azure.microsoft.com/es-mx/resources/cloud-computing-dictionary/what-is-saas/) y su uso más común es cuando se quiera detectar posibles amenazas entrantes.

#### Azure Sentinel ![sentinel](/images/icon-Azure-Sentinel.svg)

Es un servicio que "*vigila*", detecta, invesitga y recopila datos a escala de nube para poder proporcionar soluciones con inteligencia artificial. Es un servicio tipo [SaaS](https://azure.microsoft.com/es-mx/resources/cloud-computing-dictionary/what-is-saas/) y su uso recomendado es ***siempre***. Es un servicio que es **SIEM** y **SOAR** (Security, Operational, Availability, Reliability) al mismo tiempo que es un servicio de seguridad. **SIEM** es una palabra que significa "**Sistema de Información y Monitoreo**", y **SOAR** es una palabra que significa "**Sistema Operativo de Availabilidad y Reliability**". Ambos están juntos para poder hacer lo necesario (y disponible) en ajustes de seguridad.

#### Azure Key Vault ![keyVault](/images/icon-Key-Vaults.svg)

Como su nombre lo dice, es un servicio que almacena y gestiona claves, llaves o certificados (SSL) de manera cifrada (y los respalda por medio de módulos de seguridad de hardware HSM) que llega a ser muy difícil que se accedan a estos datos si no se tienen los permisos correctos. Su uso principal es para supervisar y controlar el acceso. Es un servicio tipo [SaaS](https://azure.microsoft.com/es-mx/resources/cloud-computing-dictionary/what-is-saas/).



#### Grupos de Seguridad de Red (NSG) ![NSG](/images/icon-Network-Security-Groups.svg)

Este servicio proporciona el filtrado de tráfico de red desde y hacia los recursos de redes virutales, además de aislar (si se encuentran) las máquinas virtuales y crear subredes. Es un servicio tipo [IaaS](https://azure.microsoft.com/es-mx/resources/cloud-computing-dictionary/what-is-iaas/) y su uso más común es cuando se quiera proteger una red y se pueden establecer regalas para filtrar por puerto, dirección IP o protocolo. Tales reglas se manejan por prioridades.

----

### Prerrequisitos para las prácticas
 - Tener una cuenta de Azure para realizar la práctica en su [*Portal*](https://portal.azure.com/#home) (si aún no se cuenta con alguna, se puede hacer el registro en el siguiente [*enlace*](https://azure.microsoft.com/es-mx/free/)). 
 - Contar con una suscripción activa de Azure para poder realizar la práctica (en el enlace anterior se muestra como se puede hacer).


----
### Práctica Azure Sentinel ![sentinel](/images/icon-Azure-Sentinel.svg)

#### Instrucciones

Caundo se busca dento del [Portal de Azure](https://portal.azure.com/#home) el servicio con el nombre **Microsoft Sentinel** o **Azure Sentinel**, se solicitará un área de trabajo (de [Log Analytics](https://docs.microsoft.com/es-mx/azure/azure-monitor/logs/log-analytics-overview)). Para ello, se debe entonces primero crear dicha área.

1. Se selecciona el botón de **Crear un área de trabajo** y, para teener lo básico y así comenzar a trabajar, se colocan los sigueintes datos:
    - Parámetros en Datos básicos:
        | Nombre | Valor |
        |-------|-------|
        | Suscripción | Usar la suscripción activa que se obtuvo durante los prerrequisitos. |
        | Grupo de recursos | Seleccionar el grupo de recursos que se desea asignar a el área de trabajo. (Si no se cuenta con alguno, se puede crear ahí mismo). |
        | Nombre | Asignar un nombre de área de trabajo para Azure Sentinel en minúsculas. |
        | Región | Seleccionar la región en la que se desee ubicar el servicio. |

    - Se aceptan los cambios realizados con **Revisar y crear** seguido de **Crear**.
    ![nuevaArea](/images/nuevaArea.gif)

2. Una vez creada el área de trabajo, se selecciona para poder trabajar con Azure Sentinel 
    ![áreaSentinel](/images/areaSentinel.gif)

3. Como primera vista se ve ina interfaz de Azure Sentinel, donde se puede observar los servicios de seguridad. En el panel  **Libros**, se pueden ver plantillas de consultas ya predefinidas para seguridad en los servicios de Azure.
También se pueden crear libros de consultas personalizadas.
En **MITRE ATT&CK** (que es una organización de ciberseguridad importante), se pueden ver las herramientas de seguridad que se pueden usar para crear plantillas de consultas.
![sentinel](/images/sentinel.gif)

[⚠](#⚠importante⚠)

----

### Práctica Azure Key Vault ![keyVault](/images/icon-Key-Vaults.svg)

#### Instrucciones

1. Buscar dentro del [Portal de Azure](https://portal.azure.com/#home) el servicio ***Alamcen de claves*** (o **Key Vault** si se encuentra el sitio en inglés). Se selecciona la opción de crear y como puntos importantes:
    - Parámetros en Datos básicos:
        | Nombre | Valor |
        |-------|-------|
        | Suscripción | Usar la suscripción activa que se obtuvo durante los prerrequisitos. |
        | Grupo de recursos | Seleccionar el grupo de recursos que se desea asignar. (Si no se cuenta con alguno, se puede crear ahí mismo). |
        | Nombre del almacén de claves| Asignar un nombre del almacén de claves.|
        | Región | Seleccionar la región en la que se desee ubicar el servicio. |
        |Plan de tarifa | Seleccionar el plan de tarifa que se desea usar. En este caso para fines prácticos será **Estándar**. |
        |Días durante los cuales se convervará el almacén de claves | Seleccionar el número de días durante los cuales se convervará el almacén de claves. Por default está habilitado con 90 días, pero se puede modificar **antes** de la creación de servicio.|

    - Parámetros en Directivas de Acceso (esto es importante si se busca tener un acceso a tráves de **Virtual Machines**, **Resource Managers**, o bien con **Azure Disk Encryption**).
        - Si bien, se pueden mantener las 3 opciones habilitadas.

    - Se aceptan los cambios realizados con **Revisar y crear** seguido de **Crear**.

    ![nuevoAlmacen](/images/nuevoAlmacen.gif)

2. Una vez creado el almacén de claves, se selecciona el recurso y dentro se verá una interfaz con un panel lateral izquierdo de opciones para poder administrar las claves y otros datos del almacén de claves. En ***Configuración >> Claves*** se seleccionará la opción de **Generar o importar** para poder crear una clave.
    | Parámetro | Descripción |
    |----------|------------|
    |Opciones | Seleccionar la opción de **Generar**. |
    |Nombre | Asignar un nombre para la clave. Ejemplo: **Appiskey**. |
    |Tamaño de la clave| Seleccionar el tamaño de la clave. Entre más alto sea el tamaño, más fuerte será. |

    - Se selecciona el botón **Crear** y, una vez creada la clave, se verá reflejada en la interfaz previa. Se ingresa a dicha clave y se puede descargar la llave pública para un uso futuro.
    
    ![nuevaClave](/images/nuevaClave.gif)

3. Si se requiere guardar las contraseñas, se puede hacer en el apartado **Secretos**. Se seleccionará la opción de **Generar o importar**:
    | Parámetro | Descripción |
    |----------|------------|
    |Opciones de carga | Puede ser **Manual** (ingresar la contrasñea) o bien **Certificado** (SSL). En este caso es **Manual**. |
    |Nombre | Asignar un nombre para el secreto. |
    | Valor | Asignar el valor del secreto que es la contraseña. |
    |Tipo de contenido| Se puede describir sobre qué es el secreto.|

    - Se selecciona el botón **Crear** y, una vez creado el secreto, se verá reflejado en la interfaz previa. Si se ingresa a dicho secreto, se puede **Mostrar valor secreto** para un uso futuro.
    ![nuevoSecreto](/images/nuevoSecreto.gif)

    [⚠](#⚠importante⚠)

----

### Práctica NSG ![nsg](/images/icon-Network-Security-Groups.svg)

#### Requisitos
 - Contar con **una** Maquina Virtual de Azure. Se puede guiarse con este [enlace](https://github.com/JohnNadja/Practica-VM-dentro-de-VM#requisitos) con unas modificaciones en:
    - ***Datos básicos***, ahí se cambiarán los **Puertos de entrada públicos**[*](https://github.com/JohnNadja/Practica-VM-dentro-de-VM/blob/main/images/2.2.png). Se selecciona la opción **Ninguno**.
    - ***Administración***, se selecciona en el apartado  **Supervisión** ➡ **Deshabilitar**.
    ![administracion](/images/administracion.png)

#### Instrucciones

1. Una vez creada la Máquina Virtual y, estando dentro del recurso, se irá al apartado de ***Configuración*** ➡ **Redes** (se encuentra en el panel izquierdo) y mostrará que *Esta interfaz de red no contiene grupos de seguridad*.
    ![redVM](/images/redVM.gif)

2. Ahora se requiere crear el recurso de ***Grupos de Seguridad de Red*** en el Portal de Azure. Se selecciona la opción de **Crear** y se ingresa los datos:
    - Parámtros en Datos básicos:
        | Nombre | Descripción |
        |----------|------------|
        | Suscripción | Usar la suscripción activa que se obtuvo durante los prerrequisitos. |
        |Nombre | Asignar un nombre para el grupo de seguridad. |
        |Descripción | Asignar una descripción para el grupo de seguridad de red. |
        |Región | Seleccionar la región en la que se desea ubicar el grupo de seguridad. Se recomienda que sea la misma ubicación donde se creó la Máquina Virtual|

    - Se acepatan los cambios realizados con **Revisar y crear** seguido de **Crear**.
    ![nuevoGrupo](/images/nuevoGrupo.gif)

3. Dentro del recurso de Grupos de Red de Seguridad, en su panel lateral izquierdo se irá al apartado ***Configuración*** ➡ **Interfaces de red**. Ahí se selecciona el botón **Asociar** y se selecciona la Máquina Virtual creada anteriormente.
    ![asociar](/images/asociar.gif)

4. Sin embargo, no se puede conectar aún a la Máquina virtual por el puerto deseado [que en esta ocasión será el RDP(3389)]. Entonces, desde el recurso de **Grupos de Seguridad de Red**, se agregará una **Regla de seguridad de entrada** (en el apartado de ***Configuración***).
    - Se se pulsa el botón **Agregar** con los siguientes parámetros modificados:
        |Nombre|Valor|
        |-|-|
        |Origen| Seleccionar **Any**. |
        | Intervalos de puertos de origen | Colocar un "*" (sin comillas). |
        |Destino| Seleccionar **Any**. |
        |Servicio| Seleccionar **Custom**. |
        |Intervalos de puertos de destino| Colocar un "3389" (sin comillas). |
        |Protocolo| Seleccionar **TCP**. |
        |Acción| Seleccionar **Permitir**. |
        |Prioridad| Puede dejarse en *100*, pero entre más najo sea el número, mas prioridad tendrá la regla. |
        |Nombre | Asignar un nombre para la regla. Ejemplo: *PermitirRDP*. |
    
    - Se selecciona el botón **Agregar** para finalizar la ediciónde la nueva regla de seguridad.
    ![nuevaRegla](/images/nuevaRegla.gif)

5. Una vez complatada la configuración, se puede conectar a la Máquina Virtual por el puerto RDP (con los [siguientes pasos](https://github.com/JohnNadja/Practica-VM-dentro-de-VM#acceso-a-las-m%C3%A1quinas-virtuales)). Esto se realiza con el usuario y contrasña que se asignaron en la creación de la Máquina Virtual.
     - Cuando se verifique la conexión e intalación de la máquina virtual, se puede realizar el siguiente paso.

6. La máquina virtual tiene acceso a internet de forma predeterminada, pero esto se puede deshabilitar por medio de una **Regla de seguridad de salida**. Se configura esto en el apartado de ***Configuración*** ➡ ➡ **Reglas de seguridad de salida** dentro del recurso de Grupos de Seguridad de Red.
    - Se selecciona el botón **Agregar** con los siguientes parámetros mo dificados:
        |Nombre|Valor|
        |-|-|
        |Origen| Seleccionar **Any**. |
        | Intervalos de puertos de origen | Colocar un "*" (sin comillas). |
        |Destino| Seleccionar **Service Tag**. |
        |Servicio| Seleccionar **Custom**. |
        |Etiqueta de servicio| Seleccionar **Internet**. |
        |Intervalos de puertos de destino| Colocar un "*" (sin comillas). |
        |Protocolo| Seleccionar **TCP**. |
        |Acción| Seleccionar **Denegar**. |
        |Prioridad| Puede dejarse en *110*, pero entre más najo sea el número, mas prioridad tendrá la regla. |
        |Nombre | Asignar un nombre para la regla. Ejemplo: *NoInternet*. |
    
    - Se selecciona el botón **Agregar** para finalizar la ediciónde la nueva regla de seguridad.
    ![noInternet](/images/noInternet.gif)

7. Para verificar si no hay acceso a internet en la Máquina Virtual, puede hacerse una consulta en el navegador de la misma o bien, con https://ismyinternetworking.com/.
    ![testInternet](/images/testInternet.gif)

[⚠](#⚠importante⚠)

----

# **⚠Importante⚠** 
### Recordar que, si no se requiere más del servicio, se puede eliminar pulsando el botón **Detener** después de haber seleccionado la *instancia de proceso* que, se encuentra en **Proceso** del panel izquierdo.
O bien, eliminar el grupo de recursos dentro del [Portal de Azure](https://portal.azure.com/) si no se requiere todo el contenido de dicho grupo.

----
###### <sub>[Volver al índice principal de prácticas](#índice)<sub>

## Hasta aquí la finalización de las prácticas.