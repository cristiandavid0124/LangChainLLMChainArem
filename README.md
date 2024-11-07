# AREP - Taller LLMChatGPTlive
## Autor: Cristian David Naranjo Orjuela

El propósito de este taller es desarrollar una aplicación web básica para la traducción de texto utilizando LangChain y un modelo de lenguaje LLM.

### Instalación y Ejecución
Para ejecutar la aplicación es necesario instalar Python 3.12.7 o versiones similares y git. El primer paso es clonar el repositorio e ingresar a la carpeta resultante

```
https://github.com/cristiandavid0124/RagchatGPTliveArem.git
````

en el archivo del server deve poner la clave que asigno el profe en este caso quitele la frase " holaaaaa "al inicio de la llave debido  que github no deja colocarla



```
os.environ["OPENAI_API_KEY"] = "holaaaaask-proj-CEEQHbn9kxfaeGHpJkgUOhUvLW3RnndCHwsLvRq8qH50M7tGiDnAtkufe22G0ROHRkyO0zdgDKT3BlbkFJj1FfBu3H-5AThHROq_g8XRzzrR_1fW2__YPIdUcH87UQ_gLTnTI9m6xzCebvsik2GDBnYZLCsA"
```

Luego ingrese los comandos :

```
python -m venv .venv
```

```
.venv\Scripts\activate
```

```
pip install -r requirements.txt
```

luego de la instalacion puede ejecutar el servidor con:

```
python langchainserver.py
```

Finalmente pruebe el servidor ingresando a http://localhost:8000/chain/playground/ 

![image](https://github.com/user-attachments/assets/69fc7874-8098-4006-bc81-8a9788ebcf74)




### Arquitectura

La arquitectura de esta aplicación está diseñada para permitir una interacción fluida entre el cliente y un servidor que ejecuta un modelo de lenguaje mediante solicitudes HTTP. A continuación se explica cada componente en detalle:

Cliente: El cliente es el punto de inicio en esta arquitectura. Puede interactuar con el servidor a través de solicitudes HTTP directas o mediante una interfaz de usuario proporcionada por LangServe. Esto permite que el cliente envíe datos de entrada, como el texto que desea traducir y el idioma de destino, para que el servidor los procese.

FastAPI: FastAPI actúa como el marco de backend principal que recibe y gestiona todas las solicitudes HTTP del cliente. Cuando una solicitud llega al servidor, FastAPI la dirige a los componentes adecuados de la cadena de procesamiento, asegurando una respuesta rápida y eficiente. Además, FastAPI proporciona funcionalidades de servidor web, permitiendo a la aplicación manejar múltiples solicitudes y configurar rutas de API de manera sencilla.

LangServe: LangServe es el componente que expone una API REST para el cliente, permitiendo el acceso a los servicios de procesamiento de lenguaje. LangServe se ejecuta con Uvicorn, un servidor ASGI (Asynchronous Server Gateway Interface) ligero y rápido, que maneja el flujo de solicitudes y coordina la ejecución de las distintas rutas y el manejo del servidor. Esto permite que las solicitudes del cliente se procesen de manera asincrónica, mejorando el rendimiento.

LangChain: Dentro de LangChain se encuentran los componentes que transforman y procesan las solicitudes de lenguaje natural. La cadena se construye mediante los siguientes pasos:

Prompt Template: El ChatPromptTemplate se configura para formatear las solicitudes del cliente en prompts específicos. Esto permite que las solicitudes del cliente sean adaptadas para que el modelo las procese adecuadamente, garantizando la traducción correcta al idioma especificado.
Model (ChatOpenAI): El modelo ChatOpenAI recibe el prompt formateado y genera una respuesta en función de la solicitud. Este modelo es el núcleo de procesamiento de lenguaje que realiza la tarea solicitada, como la traducción.
Parser (StrOutputParser): El StrOutputParser toma la salida del modelo y la convierte en un formato adecuado para el cliente. Este componente se asegura de que la respuesta esté estructurada y formateada correctamente antes de ser enviada de vuelta al cliente.
Cadena de Procesamiento (chain): Estos componentes se combinan en una cadena usando el operador |, formando un flujo donde:

Prompt Template procesa la entrada inicial del cliente y genera el prompt.
El Model recibe este prompt y produce la respuesta solicitada.
El Parser toma la salida del modelo y la transforma en un formato final antes de devolverla a LangServe.
RemoteRunnable: Este componente permite al cliente interactuar con el servidor de manera programática desde una ubicación remota, facilitando el envío y recepción de datos sin necesidad de interactuar directamente con el backend. RemoteRunnable realiza solicitudes HTTP a LangServe, ejecutando la cadena de procesamiento completa en el servidor y devolviendo la respuesta al cliente.



![diagramaTaller](https://github.com/user-attachments/assets/705276b8-4b90-4039-976d-a852f594b22b)




