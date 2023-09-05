# Persistent start

Please ensure the target volume (`~/kui/config.yml`) of your config file does exist.

Create a yml file with the following contents:

```
services:
  kafka-ui:
    container_name: kafka-ui
    image: provectuslabs/kafka-ui:latest
    ports:
      - 8080:8080
    environment:
      DYNAMIC_CONFIG_ENABLED: true
    volumes:
      - ~/kui/config.yml:/etc/kafkaui/dynamic_config.yaml
```

Run the compose via:

`docker-compose -f <your-file>.yml up -d`
