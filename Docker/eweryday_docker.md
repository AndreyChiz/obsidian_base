`docker rmi $(docker images -aq)` : удалить все образы
`docker rmi $(docker images -f "dangling=true" -q)` :удалить все образы у которых нет имени

