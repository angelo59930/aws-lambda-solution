# AWS LAMBDA SOLUTION

## Descripción
Este proyecto implementa un servicio en AWS Lambda utilizando CloudFormation. El servicio procesa peticiones GET y devuelve un mensaje de bienvenida.

La implementación de la solución se realizó utilizando el siguiente conjunto de tecnologías:
- AWS Lambda
- AWS API Gateway
- AWS CloudFormation
- GitHub Actions
- Python

## Configuración
Para configurar el servicio en AWS Lambda, se debe seguir los siguientes pasos:

### Pre-requisitos
- Contar con una cuenta en AWS.
- Contar con un repositorio en GitHub.
  
### Pasos
1. Ingrear a la cuenta de AWS.
2. Crear un grupo de con los permisos necesarios para ejecutar el servicio de AWS SAM. En nuestro caso utilizaremos **AdministratorAccess**
3. Crear un usuario de AWS que use el grupo anteriormente creado.
4. Generar las credenciales de acceso para el usuario creado (Access Key ID y Secret Access Key).
5. Crear un secreto en GitHub con las credenciales generadas en el paso anterior.

Las credenciales generadas deben llamarse `AWS_ACCESS_KEY_ID` y `AWS_SECRET_ACCESS_KEY`.

A su vez se crea un secreto mas llamado `AWS_REGION` con el valor de la región en la que se desplegará nuestra app.

## Uso
Para utilizar el servicio, se debe realizar una petición GET al endpoint generado por el API Gateway. El servicio devolverá un mensaje de bienvenida.

Generalmente el formato de la url es el siguiente:
```
https://<api-id>.execute-api.<region>.amazonaws.com/Prod/hello
```

Para obtener la url del servicio, se debe ingresar a la consola de AWS y buscar el servicio API Gateway. En la sección de APIs, se debe seleccionar el API creado y copiar la url generada.

### Ejemplo
Petición:
```
curl --location 'https://ht6cbyfm59.execute-api.us-east-1.amazonaws.com/Prod/hello'
```

Respuesta esperada:
```
"¡Hola desde AWS Lambda! Mi nombre es ..."
```

## Expliación de la solución
La solución implementada consta de los siguientes componentes:
- **Lambda Function**: Función que procesa las peticiones GET y devuelve un mensaje de bienvenida.
- **API Gateway**: API que expone la función Lambda para ser consumida por los clientes.
- **CloudFormation**: Plantilla que define los recursos necesarios para implementar la solución.
- **GitHub Actions**: Flujo de trabajo que automatiza la implementación de la solución en AWS.
- **Python**: Lenguaje de programación utilizado para el desarrollo de la función Lambda.

El template de AWS SAM se encarga de definir los recursos necesarios para implementar la solución. En este caso, se definen una función Lambda y un API Gateway.

El api gateway se encarga de exponer la función Lambda para ser consumida por los clientes. La función Lambda procesa las peticiones GET y devuelve un mensaje de bienvenida.

El flujo de trabajo de GitHub Actions se activa cuando se realiza un push en la rama main del repositorio. El flujo de trabajo se encarga de:
1. Utilizar la versión de Python 3.8.
2. Setear las credenciales de AWS.
3. Generar el build del proyecto con `sam build`.
4. Generar el deploy del proyecto con `sam deploy`.

### Tener en cuenta
- La plantilla de CloudFormation se encuentra en el archivo `template.yaml`.
  En el archivo se definen los recursos necesarios para implementar la solución.
  como la función Lambda, el API Gateway, donde se encuentra el handler del lambda, etc.
- El código de la función Lambda se encuentra en el archivo `app/app.py`.
- El pipeline se creo siguiendo la documentación oficial de GitHub Actions y AWS. Si se desea tener mas informacion
puede dirigirse a [Deploying using GitHub Actions](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/deploying-using-github.html)

## Bibliografía
- [¿Qué es el AWS Serverless Application Model (AWS SAM)?](https://docs.aws.amazon.com/es_es/serverless-application-model/latest/developerguide/what-is-sam.html)
- [GitHub Actions](https://docs.github.com/es/actions/quickstart)
- [Using GitHub Actions to deploy serverless applications](https://aws.amazon.com/es/blogs/compute/using-github-actions-to-deploy-serverless-applications/)
- [Deploying using GitHub Actions]((https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/deploying-using-github.html))
