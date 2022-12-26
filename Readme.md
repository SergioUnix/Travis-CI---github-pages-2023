----------- Para el Fronted
--crear imagen para fronted
   docker build -t sergiounix/chino_imagen_python .

  --publicar en docker hub la imagen creada
   docker push sergiounix/chino_imagen_python



-- crear contenedor para la imagen 
  docker run -d -p 3200:3100 --name micro-admin sergiounix/chino_imagen_python

  docker network create microservicios
  docker run -d -p 0.0.0.0:3200:3100 --network=microservicios --name micro-admin sergiounix/chino_imagen_python


docker run -d -p 8080:3100 --name micro-admin sergiounix/chino_imagen_python



-----------------------------------Delete contenedores e Imagenes
---parar todos los contenedores de docker corriendo
docker stop $(docker ps -a -q)

--eliminar todos los contenedores de docker parados
docker rm $(docker ps -a -q)


--eliminar todas las imagenes de docker 
docker rmi $(docker images -a -q)



--Instalar docker en ubuntu
https://docs.docker.com/engine/install/ubuntu/

---instalar gitlab-runner en Compute engine para ubuntu
https://docs.gitlab.com/runner/install/linux-repository.html


curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash






# para Subir a Cloud run

--- Para cloud Run
1. primero tener subida la imagen a docker hub
2. luego acceder a la shell de google cloud
3. jalamos la imagen 
   docker pull sergiounix/chino_imagen_python
4. ahora enviarla al registro privado de google ---------'lithe-realm-371920'=id del proyecto en el que estoy   ... 'back-rust'  nuevo nombre de la imagen
   docker tag sergiounix/chino_imagen_python gcr.io/lithe-realm-371920/servi:v1
5. revisamos si esta    
  docker image ls
6. antes de enviar la imagen debemos de dar permisos para poder empujar la imagen
   Nos dirigimos a container Registry Api y lo habilitamos
7. tomamos la imagen y la empujamos ya renombrada , al registro privado
   docker push gcr.io/lithe-realm-371920/servi:v1
8. ahora ya esta disponible en todos los recursos de google cloud

9. luego ir a Docker run para correr mi contenedor