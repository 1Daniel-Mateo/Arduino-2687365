# PROGRAMACION ARDUINO 2

### Potenciometro

El potenciometro es un componente eletronico en cual podemos el controlar flujo de energia que se transmite en el circuito, como si fuera un presa que permite cierto paso de corrientes del agua, que puede girar en sentido horario y antihorario.

los pines genericos de este componente son el a,b y c. 

a: Es el que corresponde a tierra

b: Corresponde a la entrada de señal al circuito y a la transmicion de flujo energetico

c: Corresponde a la señal de entrada es la que controla el flujo de energia en el circuito

cuando se gire en sentido horario se reducira la resistencia de pin b y permitira mas flujo electrico en el pin a.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/642d307e-07f4-4398-b6ea-21bf3264dfc4/f6a825ed-52f2-402d-bd2a-294e494c43ce/Untitled.png)

cuando se gire en sentido antihorario se aumentara la resistencia en pin b y reducira en pin a flujo electrico al circuito.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/642d307e-07f4-4398-b6ea-21bf3264dfc4/d8e85bcc-63b5-4169-b25f-74a670b1e753/Untitled.png)

dependiendo el cambio de horario en le potenciometro este hara la interrupcion con pin b ya que este es su resistencia.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/642d307e-07f4-4398-b6ea-21bf3264dfc4/faa5f5cf-5f8d-42ea-bca4-bfc659f69ebc/Untitled.png)

CODIGO DE PRUEBA DE PONTENCIOMETRO

En este condigo mide la potencia y nos muestra graficamente el flujo de energia en la cual imprimira en caso de que vaya en la forma horaria nos mostrara que aumenta a numeros positivos mostrando que se reduce la resistencia en el puerto b.

si es anti horario reducira el flujo de energia que pasa por el circuito y se imprimira en negativo

### Explicacion del codigo

1. Definimos las variables A y B como los pines de la placa arduino que son el pin 2 y 4 y donde seran las señales
2. Definimos las variables anterior y posicion para que tenga un indicio de conteo de 50 que aumenta y disminuira en la consola
3. En el motodo setup, traeremos las variables para que reconozca sa que pines nos dirijemos y que estamos enviendo para que realize una accion y que la linea “attachInterrupt(digitalPinToInterrupt(A), encoder, LOW);” tenga la funcion de interrupir e imprimir en la consola llamando al metodo encoder.
4. en el metodo loop le decimos que si la  posicion es diferente a la variable llamada anterior no imprima la posicion y que diga que anterior es igual la variable posicion.
5. en el metodo encoder, va a traer las posiciones y va a imprimirlas, teniendo en cuenta lo millios que cuando interrumpamos con el potenciometro usara la condicion para decrementar si va en sentido antihorario y aumentar si va en sentido antihorario y definiremos la posicion como minimo en 100 y el max en 0. Tambien diremos que la variable interrupcion es igual al tiempo de interrupcion.

1. prueba exitosa 

Sentido Antihorario

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/642d307e-07f4-4398-b6ea-21bf3264dfc4/de11c647-d1b1-4247-a88b-3c1002b01475/Untitled.png)

Sentido horario

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/642d307e-07f4-4398-b6ea-21bf3264dfc4/e0936cb9-4430-4798-bdb7-10d912c96410/Untitled.png)

Codigo del programa de potenciometro:

```jsx
int A = 2;
int B = 4;

int anterior = 50;
volatile int posicion = 50;

void setup() {
  pinMode(A, INPUT);
  pinMode(B, INPUT);

  Serial.begin(9600);

  attachInterrupt(digitalPinToInterrupt(A), encoder, LOW);

  Serial.println("Listo");

}

void loop() {
  if (posicion != anterior) {
    Serial.println(posicion);
    anterior = posicion;
  }

}

void encoder(){
  static unsigned long ultimaInterrupcion = 0;
  unsigned long tiempoInterrupcion = millis();

  if (tiempoInterrupcion - ultimaInterrupcion > 5 ) {
    if (digitalRead(B) == HIGH) {
      posicion++;
    }else {
      posicion--;
    }

    posicion = min(100, max(0, posicion));

    ultimaInterrupcion = tiempoInterrupcion;
  } 

}
```
