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
    
    solicita_pin --> realizar_transaccion: Pin correcto
    solicita_pin --> solicita_pin: Pin incorrecto(intento < 3).
    solicita_pin --> solicita_pin: pin incorrecto (3 intentos).
    solicita_pin --> standby: ingreso mal el pin 3 veces.
    
    realizar_transaccion --> elegir_transaccion: Usuario elige transacción.
    elegir_transaccion --> realizar_transaccion: Ha elegido una transacción.
    realizar_transaccion --> elegir_transaccion: Ha escodigo realizar otra transacción.
    realizar_transaccion --> standby: Ha elegido finalizar.
    @enduml

  ![image](https://github.com/user-attachments/assets/82576ba8-94a9-4cd6-9f4d-a19521ddd0a8)




