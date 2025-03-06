## Diagrama de estado: ACTIVIDAD 6.3.2 - CAJERO

#### Trabajo a realizar
Diagrama de estados, que refleje los distintos estados y transiciones en los que se encuentra el cajero en cada momento:
- El funcionamiento general de un cajero es el siguiente:
    - El sistema en un estado stand-by hasta que un usuario introduce una tarjeta.
    - El usuario introduce la tarjeta en el sistema y el sistema valida la tarjeta. Si la tarjeta no es correcta, el sistema expulsará la tarjeta y quedará en estado stand-by. En el caso de ser una tarjeta válida, el sistema solicita al usuario que se valide mediante un pin. 
    - Si hay error en el pin, el sistema volverá al usuario que vuelva a intentar validarse hasta completar el proceso 3 veces, en cuyo caso, si el usuario no se ha validado correctamente finalizará el proceso, quedándose con la tarjeta. El usuario podrá cancelar el proceso de identificación en cualquier momento antes de cumplir los 3 intentos. 
    - Una vez el usuario se ha validado correctamente, el sistema ofrecerá al sistema las distintas transacciones que puede realizar. Cuando una transacción sea elegida, se llevará a cabo, y, al finalizarla, el sistema dará la opción de poder elegir una nueva transacción o cancelar la interacción con el cajero y por tanto finalizar sesión. La interacción con el cajero podrá ser cancelada, finalizada la sesión, en cualquier momento siempre y cuando no esté en proceso de ejecución de una transacción. 

#### PlantUML:
        @startuml
    [*] --> standby
    standby --> validar_tarjeta: tarjeta introducida
    validar_tarjeta --> solicita_pin: tarjeta correcta
    validar_tarjeta --> standby: tarjeta incorrecta.
    
    solicita_pin --> elegir_transaccion: Pin correcto
    solicita_pin --> solicita_pin: Pin incorrecto(intento < 3)
    solicita_pin --> solicita_pin: pin incorrecto (3 intentos)
    solicita_pin --> standby: ingreso mal el pin 3 veces.
    
    elegir_transaccion --> realizar_transaccion: Usuario elige una transaccion
    realizar_transaccion --> elegir_transaccion: Ha elegido realizar otra transaccion
    realizar_transaccion --> standby: Ha elegido finalizar.
    @enduml

  ![image](https://github.com/user-attachments/assets/82576ba8-94a9-4cd6-9f4d-a19521ddd0a8)


#### Interpretación del diagrama.
- Siguiendo la lógica del cajero, por defecto, al iniciar, se encontrará en standby a la espera de que un usuario introduzca una tarjeta.

- Si la tarjeta introducida no es válida, volverá a estar en standby a la espera de ingresar otra tarjeta.

- Volverá a validar hasta que detecte una tarjeta válida. Cuando lo sea, solicitará un pin al usuario que debe ingresar.

- Si el usuario introduce bien el pin, pasará a elegir una transacción. Si introduce mal el pin tendrá hasta 3 intentos para ingresarlo bien, lo cual volverá a pedir pin hasta 3 veces. 
- Si el usuario ingresa mal el pin 3 veces, pasará a estar en standby el cajero.

- Cuando el usuario elija una transacción, preguntará si quiere realizar otra o si quiere salir. 

- Si elige hacer otra, volver a pedir una transacción, si elige salir, el cajero pasará a estar de nuevo en standby a la espera de otra tarjeta.


