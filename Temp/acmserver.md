```shell
sudo mount /dev/sdb1 /home/disk1
sudo mount /dev/sdc1 /home/disk2
cd /home/judge/jnoj
cd judge
sudo pkill -9 dispatcher
make
sudo ./dispatcher -o
cd ../polygon
sudo pkill -9 polygon
make
sudo ./polygon
```

