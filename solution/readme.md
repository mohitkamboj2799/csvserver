cmd for part - docker pull infracloudio/csvserver:latest
docker run -d --name csvserver_container infracloudio/csvserver:latest
docker ps

nano gencsv.sh

#!/bin/bash

start=$1
end=$2

for ((i = start; i <= end; i++)); do
echo "$i, $((RANDOM % 100))" >> inputFile
done
chmod +x gencsv.sh
./gencsv.sh 2 8
./gencsv.sh 2 8
docker stop csvserver_container
docker rm csvserver_container
docker run -d --name csvserver_container -v $(pwd)/inputFile:/csvserver/inputdata infracloudio/csvserver:latest

docker exec -it csvserver_container /bin/bash

netstat -tulpen | grep LISTEN
exit
docker stop csvserver_container
docker rm csvserver_container
docker run -d --name csvserver_container -e CSVSERVER_BORDER=Orange -p 9393:9300 -v $(pwd)/inputFile:/csvserver/inputdata infracloudio/csvserver:latest
