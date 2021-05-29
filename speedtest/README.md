## 100MBの書き出しで速度比較

### docker-sync無し

```
$ make run-without-docker-sync
Creating speedtest_app_run ... done
102400+0 records in
102400+0 records out
104857600 bytes (100.0MB) copied, 67.635562 seconds, 1.5MB/s
real    1m 7.63s
user    0m 0.16s
sys     0m 5.23s
```

### docker-sync有り

```
$ make start-sync
$ make run-with-docker-sync
make run-with-docker-sync
Creating speedtest_app_run ... done
102400+0 records in
102400+0 records out
104857600 bytes (100.0MB) copied, 0.288115 seconds, 347.1MB/s
real    0m 0.28s
user    0m 0.01s
sys     0m 0.26s
```
