# p-dc-hivemind

steem hivemind

## 사전 작업

- fullnode + jussi 설치가 완료된 이후 작업 진행을 하는 것을 추천함.
- 물론 공홈 API를 호출하여 하이브마인드만 구축할 수 있으나. 공홈 API에 많은 부하를 줌

## 설정

`docker-compose.yml`

> STEEMD_URL: https://your.steemapi.url

- 위 주소 정보를 jussi 에서 설정한 domain 정보로 바꿔주면 됨.
  ( 공홈 API https://api.steemit.com 을 사용하는 것은 비추천, database-lock을 발생시키는 주범이 됨;; 한번에 block을 1000개씩 지속적으로 pulling 하기 때문)
- 내부적으로 보면 해당 rpc api call 을 지속적으로 하면서 데이터를 받아오는 것이므로 `jussi_num` 이 지속적으로 update 되는 것을 확인할 수 있다.

## requirements

> For a system with 16G of memory, here's a good start:

```txt
effective_cache_size = 12GB # 50-75% of avail memory
maintenance_work_mem = 2GB
random_page_cost = 1.0      # assuming SSD storage
shared_buffers = 4GB        # 25% of memory
work_mem = 512MB
synchronous_commit = off
checkpoint_completion_target = 0.9
checkpoint_timeout = 30min
max_wal_size = 4GB
```

## adminer 추가 및 삭제

adminer : 손쉽게 db를 확인/조작할 수 있도록 도와주는 web app

```yml
adminer:
  image: adminer
  restart: always
  ports:
    - 7777:8080
```

adminer 를 yml 에 추가 이후 삭제하는 경우 `WARNING: Found orphan containers ...` 이런 메시지가 출력되는데 이런 경우 컨테이너 종료 시 아래와 같이 입력하면 컨테이너에서 존재하지 않는 service 는 제거 해줘서 다음부터는 경고 메시지가 출력되지 않는다.

`docker-compose down --remove-orphans`

## reference

- [hivemind 搭建教程](https://steemit.com/cn/@ety001/hivemind)
- [steemit : hivemind](https://github.com/steemit/hivemind)
