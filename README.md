## Задачи по процессам

1. Опишите, что происходит, при выполнении любой команды в консоли, например:
    `$ ls -l` 

    Происходит вызов `fork()` посредством которого оболочка клонирует себя, далее в новосозданном дочернем процессе происходит вызов `exec()`, для непосредественно вызов программы `ls` с ключом `-l`. После заверения работы программы `ls`, дочерний процесс оболочки заверщается и передаёт вывод и управление родительскому процессу

2. Используя ключ 'o', выведите с помощью `ps` список всех процессов в таком формате:
    `PID USER     %CPU    VSZ TT       COMMAND`
    пояснение: ID процесса, пользователь (real user), % загрузки CPU, размер виртуальной памяти, управляющий терминал, команда

    прикрепите вывод к задаче, перенаправив вывод на `head`:

    `ps -d -o pid,user,pcpu,vsize,tty,comm | head`

| PID | USER | %CPU |VSZ | TT | COMMAND |
|---------:|:---------:|:---------:|:---------:|:---------:|:---------|
| 2 | root | 0.0 |  0 | ? | kthreadd |
| 3 | root | 0.0 |  0 | ? | rcu_gp |
| 4 | root | 0.0 |  0 | ? | rcu_par_gp |
| 6 | root | 0.0 |  0 | ? | kworker/0:0H-kblockd  |
| 7 | root | 0.0 |  0 | ? | kworker/u256:0-events_unbound  |
| 8 | root | 0.0 |  0 | ? | mm_percpu_wq |
| 9 | root | 0.0 |  0 | ? | ksoftirqd/0 |
| 10 | root | 0.0 |  0 | ? | rcu_sched |
| 11 | root | 0.0 |  0 | ? | rcu_bh |


3. Создайте процесс sleep с помощью 
	    `$ sleep infinity &`

    `root@deb2:/home/deployer# sleep infinity &`  
    `[1] 1005`  
    
   - найдите его в списке процессов с помощью `ps`.  

    `root@deb2:/home/deployer# ps aux | grep sleep`  
    `root       1005  0.0  0.0   5260   752 pts/0    S    14:00   0:00 sleep infinity`  
    `root       1010  0.0  0.0   6076   892 pts/0    S+   14:00   0:00 grep sleep`  

   - отфильтруйте вывод `ps` чтобы получить строку только с этим процессом.

    `root@deb2:/home/deployer# ps aux | grep sleep | grep -v "grep"`  
    `root       1005  0.0  0.0   5260   752 pts/0    S    14:00   0:00 sleep infinity`  

   - убейте процесс, отправив ему сигнал '-9' программой `kill`.  

    `root@deb2:/home/deployer# ps aux | grep sleep | grep -v "grep" | awk '{print $2}' | xargs kill -9`  
    `[1]+  Killed                  sleep infinity`

   - убедитесь, что процесса больше нет в списке выдачи `ps`.  

    `root@deb2:/home/deployer# ps aux | grep sleep | grep -v "grep"`  
    `root@deb2:/home/deployer#`
