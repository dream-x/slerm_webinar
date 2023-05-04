# Инструкция к вебинару

Нужно скачать / установить:
- docker (я надеюсь он у вас по дефолту есть :))
- Patroni. git clone https://github.com/zalando/patroni.git
- [Pumba](https://github.com/alexei-led/pumba/releases) (brew install pumba) https://github.com/alexei-led/pumba
- [ChaosBlade](https://github.com/chaosblade-io/chaosblade) (docker pull chaosbladeio/chaosblade-demo)


# Примеры команд

```
pumba netem --tc-image gaiadocker/iproute2  -d 100s loss -p 15 -c 10 demo-patroni3
```

```
pumba netem --tc-image gaiadocker/iproute2  -d 100s loss -p 100 -c 90 demo-patroni1
```

```
pumba netem --tc-image gaiadocker/iproute2  -d 20s corrupt 10 -с 90 demo-patroni3е
```

```
pumba netem -d 100s delay --time 4000 demo-patroni3е
```

1. Атака - загрузка CPU
    1. ./blade create cpu load --cpu-count 1 --cpu-percent 100
    2. ./blade destroy ...
2. Атака на память
    1. ./blade create mem load --mem-percent 85
3. Атака - потеря пакетов в сети
    1. ./blade create network delay --destination-ip 10.211.55.2 --time 200 --interface enp0s5
4. ./blade server start
   1. curl "http://<ip>:9526/chaosblade?cmd=create%20cpu%20load%20--cpu-percent%2070"
   2.  curl "http://<ip>:9526/chaosblade?cmd=destroy%20abb247773fd2f958"
