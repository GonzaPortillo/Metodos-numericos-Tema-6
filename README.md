# Solución de Ecuaciones Diferenciales

## INDICE
1. [Introduccion](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/blob/main/README.md#introduccion)
2. [Algoritmos](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/blob/main/README.md#algroitmos)
3. [Implementación en Java](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/blob/main/README.md#implementación-en-java)
   * [Euler](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/blob/main/README.md#euler-1)
   * [Runge Kutta](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/blob/main/README.md#runge-kutta-1)
   * [Taylor](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/blob/main/README.md#taylor-1)
5. [Problemas](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/blob/main/README.md#problemas)
6. [Resultados de compilación](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/blob/main/README.md#resultados-de-compilación)
7. [Conclusión](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/blob/main/README.md#resultados-de-compilación)

## Introduccion
La solución de ecuaciones diferenciales en métodos numéricos se refiere a la implementación de técnicas computacionales para encontrar soluciones aproximadas a ecuaciones diferenciales, ya sean ordinarias o parciales, cuando no es posible obtener una solución analítica cerrada.

Algunos de los algoritmos que veremos son:

1. Euler: Es un método de integración numérica de primer orden para resolver ecuaciones diferenciales ordinarias. Aproxima la solución paso a paso, utilizando la pendiente inicial de la ecuación diferencial.
2. Runge Kutta: Es un método de integración numérica de orden superior (por ejemplo, Runge-Kutta de cuarto orden) para resolver ecuaciones diferenciales ordinarias. Utiliza una combinación de evaluaciones de la ecuación diferencial en diferentes puntos para obtener una aproximación más precisa.
3. Taylor: Es un método numérico para resolver ecuaciones diferenciales ordinarias. Se basa en expandir la solución de la ecuación diferencial en una serie de Taylor alrededor de un punto.

## Algroitmos

### Euler
#### Formula
![image](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/assets/160778946/222f07fa-4e45-4e9a-9aca-80f490488f1a)

1. Definir la ecuación diferencial de primer orden que se desea resolver: dy/dx = f(x, y).
2. Especificar el punto inicial (x0, y0).
3. Especificar el tamaño del paso h.
4. Calcular los valores de y en los puntos sucesivos utilizando la fórmula de Euler: ( y(n+1) = yn + h * f(xn, yn) )
5. Repetir el paso 4 hasta alcanzar el punto final deseado.

### Runge Kutta
#### Formula
![image](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/assets/160778946/8bbc811f-ca20-4216-8bd0-2c8a603291d1)

1. Definir la ecuación diferencial de primer orden que se desea resolver: dy/dx = f(x, y).
2. Especificar el punto inicial (x0, y0).
3. Especificar el tamaño del paso h.
4. Calcular los valores de y en los puntos sucesivos utilizando la fórmula de Runge-Kutta de cuarto orden.
5. Repetir el paso 4 hasta alcanzar el punto final deseado.

### Taylor
#### Formula
![Aproximacion-de-Taylor_editado](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/assets/160778946/69a98991-917b-4491-89c8-1649c6fd0b6b)

1. Definir la ecuación diferencial de primer orden que se desea resolver: dy/dx = f(x, y).
2. Especificar el punto inicial (x0, y0).
3. Calcular las derivadas de la función f(x, y) con respecto a y en el punto inicial.
4. Utilizar la serie de Taylor para aproximar la solución de la ecuación diferencial en los puntos sucesivos.
5. Repetir el paso 4 hasta alcanzar el punto final deseado.

## Implementación en Java
### Ecuacion diferencial a resolver
![image](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/assets/160778946/231fd2e9-e55d-46c5-b028-41763d78af74)

### Euler

    public class MetodoEuler {

        // Definimos la ecuación diferencial dy/dx = f(x, y)
        // En este ejemplo, vamos a usar dy/dx = x + y
        public static double f(double x, double y) {
            return x + y;
        }

        // Método de Euler
        public static void metodoEuler(double x0, double y0, double h, int n) {
            double x = x0;
            double y = y0;

            System.out.printf("x0: %.4f, y0: %.4f%n", x, y);

            // Iteramos n veces para obtener las aproximaciones
            for (int i = 0; i < n; i++) {
                y = y + h * f(x, y);
                x = x + h;

                System.out.printf("x%d: %.4f, y%d: %.4f%n", i + 1, x, i + 1, y);
            }
        }

        public static void main(String[] args) {
            // Valores iniciales
            double x0 = 0.0;
            double y0 = 1.0;
            // Tamaño del paso
            double h = 0.1;
            // Número de iteraciones
            int n = 10;

            // Llamamos al método de Euler
            metodoEuler(x0, y0, h, n);
        }
    }

### Runge Kutta

    public class RungeKutta {

        // Definimos la ecuación diferencial dy/dx = f(x, y)
        // En este ejemplo, vamos a usar dy/dx = e^x - y
        public static double f(double x, double y) {
            return Math.exp(x) - y;
        }

        // Método de Runge-Kutta de cuarto orden
        public static void metodoRungeKutta(double x0, double y0, double h, int n) {
            double x = x0;
            double y = y0;

            System.out.printf("x0: %.4f, y0: %.4f%n", x, y);

            // Iteramos n veces para obtener las aproximaciones
            for (int i = 0; i < n; i++) {
                double k1 = h * f(x, y);
                double k2 = h * f(x + h / 2.0, y + k1 / 2.0);
                double k3 = h * f(x + h / 2.0, y + k2 / 2.0);
                double k4 = h * f(x + h, y + k3);

                y = y + (k1 + 2 * k2 + 2 * k3 + k4) / 6.0;
                x = x + h;

                System.out.printf("x%d: %.4f, y%d: %.4f%n", i + 1, x, i + 1, y);
            }
        }

        public static void main(String[] args) {
            // Valores iniciales
            double x0 = 0.0;
            double y0 = 1.0;
            // Tamaño del paso
            double h = 0.1;
            // Número de iteraciones
            int n = 10;

            // Llamamos al método de Runge-Kutta
            metodoRungeKutta(x0, y0, h, n);
        }
    }

### Taylor

    public class Taylor {
        // Definimos la ecuación diferencial dy/dx = f(x, y)
        // En este ejemplo, vamos a usar dy/dx = x^2 - y
        public static double f(double x, double y) {
            return x * x - y;
        }

        // Definimos la primera derivada parcial de f con respecto a x
        public static double dfdx(double x, double y) {
            return 2 * x;
        }

        // Definimos la primera derivada parcial de f con respecto a y
        public static double dfdy(double x, double y) {
            return -1;
        }

        // Método de Taylor de segundo orden
        public static void metodoTaylor(double x0, double y0, double h, int n) {
            double x = x0;
            double y = y0;

            System.out.printf("x0: %.4f, y0: %.4f%n", x, y);

            // Iteramos n veces para obtener las aproximaciones
            for (int i = 0; i < n; i++) {
                double y1 = y + h * f(x, y) + (h * h / 2) * (dfdx(x, y) + f(x, y) * dfdy(x, y));
                y = y1;
                x = x + h;

                System.out.printf("x%d: %.4f, y%d: %.4f%n", i + 1, x, i + 1, y);
            }
        }

        public static void main(String[] args) {
            // Valores iniciales
            double x0 = 0.0;
            double y0 = 1.0;
            // Tamaño del paso
            double h = 0.1;
            // Número de iteraciones
            int n = 10;

            // Llamamos al método de Taylor
            metodoTaylor(x0, y0, h, n);
        }
    }

## Problemas 

Las siguientes ecuaciones diferenciales son resueltas con la implementacion de los 3 algoritmos. 

![image](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/assets/160778946/3c07e1c2-065f-4bca-82f9-4e5317c421b6)

A continuacion podras encontrar los 5 codigos para cada uno de los 3 metodos

* [Euler](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/tree/main/Euler)
* [Runge Kutta](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/tree/main/Runge%20Kutta)
* [Taylor](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/tree/main/Taylor)

## Resultados de compilación
### Ecuacion diferencial resuelta
![image](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/assets/160778946/231fd2e9-e55d-46c5-b028-41763d78af74)

### Euler

![image](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/assets/160778946/7dbf39c2-1625-4fbc-97e1-399d67d9f9a7)

### Runge Kutta

![image](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/assets/160778946/41df9d7e-9585-4a4a-8ca7-bda177137b6a)

### Taylor

![image](https://github.com/GonzaPortillo/Metodos-numericos-Tema-6/assets/160778946/9e6a689d-f4c8-4a42-a75b-6b638c8e836d)

## Conclusión

La solución de ecuaciones diferenciales mediante métodos numéricos es una parte integral de los métodos numéricos y es esencial para abordar problemas en ciencia, ingeniería y matemáticas donde las soluciones analíticas no son factibles. Las ecuaciones diferenciales se dividen en dos categorías principales: ordinarias (EDO) y parciales (EDP), y ambos tipos requieren enfoques específicos para su resolución numérica.
