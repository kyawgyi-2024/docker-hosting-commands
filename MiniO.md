# Pull the MinIO image (downloads the specified version)
docker pull minio/minio:RELEASE.2025-04-22T22-12-26Z

# Run MinIO container
docker run -p 9000:9000 -p 9001:9001 \        # expose ports
 --name minio-local \                         # container name
 -v ~/minio-data:/data \                      # persistent storage
 -e "MINIO_ROOT_USER=minioadmin" \            # admin username
 -e "MINIO_ROOT_PASSWORD=minioadmin" \        # admin password
 minio/minio:RELEASE.2025-04-22T22-12-26Z \   # exact MinIO version
 server /data --console-address ":9001"       # use /data and UI on 9001


### Explanation (quick + minimal)

# docker pull → downloads the MinIO image

# docker run → starts the container

# -p 9000:9000 → MinIO S3 API (for apps)

# -p 9001:9001 → MinIO Web Console (UI)

# --name minio-local → easier management

# -v ~/minio-data:/data → keeps files even after container removal

# MINIO_ROOT_USER / PASSWORD → login credentials

# server /data → storage path

# --console-address ":9001" → UI accessible at port 9001

# http://localhost:9001
# http://localhost:9000



# user: minioadmin
# pass: minioadmin

docker start minio-local    # start MinIO
docker stop minio-local     # stop MinIO
docker logs minio-local     # show logs
docker rm minio-local       # remove container

