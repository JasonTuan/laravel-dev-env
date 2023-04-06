# laravel-dev-env
Docker composer for Laravel develop environment

How to get docker-compose to always re-create containers from fresh images?
docker-compose rm -f
docker-compose pull
docker-compose up --build -d
# Run some tests
./tests
docker-compose stop -t 1