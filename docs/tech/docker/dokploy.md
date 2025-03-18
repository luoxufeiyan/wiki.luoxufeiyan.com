# Dokploy

## Compose 

Compose 文件后面需要添加dokploy网络

```yaml
    networks:
      - dokploy-network
networks:
  dokploy-network:
    external: true
```


如果需要挂载Volume的话，需要写成 `../files` 的格式

```yaml
volumes:
  - "../files/my-database:/var/lib/mysql" ✅
  - "../files/my-configs:/etc/my-app/config" ✅
```

ref: https://docs.dokploy.com/docs/core/docker-compose#advanced