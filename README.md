Backup data n8n (dalam 1 folder n8n)

docker run --rm -v n8n_n8n_data:/data -v "C:/Users/WIN10/OneDrive/Documents/App/App - n8n/n8n/backup_n8n:/backup" alpine sh -c "cp -r /data/* /backup"

Restore (dalam 1 folder n8n)

docker run --rm -v n8n_n8n_data:/data -v "${PWD}/backup_n8n:/backup" alpine sh -c "cp -r /backup/* /data"
docker compose down
docker compose up -d

Error Permision 
docker run --rm -it -v n8n_n8n_data:/data alpine sh

chown -R 1000:1000 /data
chmod -R u+rwX /data

exit

docker compose up -d
