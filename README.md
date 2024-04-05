### Работа с mdadm
### Задание: 
## добавить в Vagrantfile еще дисков;
## сломать/починить raid;
## собрать R0/R5/R10 на выбор;
## прописать собранный рейд в конф, чтобы рейд собирался при загрузке;
## создать GPT раздел и 5 партиций.
### Сдать:
## измененный Vagrantfile - присутствует в данном репозитории
## скрипт для создания рейда - 
## sudo lshw -short | grep disk
## mdadm --zero-superblock --froce /dev/sd{b,c,d,e,a}
## mdadm --create --verbose /dev/md0 -l 6 -n 5 /dev/sd{b,c,d,e,a}
## cat /proc/mdstat
## mdadm -D /dev/md0
## mdadm --detail --scan --verbose
## echo "DEVICE pertitions" > /etc/mdadm/mdadm.conf
## mdadm --detail --scan --verbose | awk '/ARRAY/{print}' >> /etc/mdadm/mdadm.conf
## parted -s /dev/md0 mklable gpt
## for i in $(seq 1 5); do sudo mkfs.ext4 /dev/md0p$i; done
## mkdir -p /raid/part{1,2,3,4,5}
## for i in $(seq 1 5); do mount /dev/md0p$i/ raid/part$i; done
## конф для автосборки рейда при загрузке - 
## cat /etc/mdadm/mdadm.conf
## ARRAY /dev/md/0 level-raid6 num-devices=5 metadata=1.2 name=otuslinux:0 UUID=784a99f2:e8d76ab0:402f66cf:b2f87560

