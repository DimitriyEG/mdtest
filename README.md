```
root@deb2:/home/deployer/isolate# sudo chroot .  
bash-5.0# ls  
bin  lib  lib64  

bash-5.0# ls -lsh  
total 12K
4.0K drwxr-xr-x 2    0    0 4.0K Jul 11 11:44 bin  
4.0K drwxr-xr-x 3 1000 1000 4.0K Jul 10 10:34 lib  
4.0K drwxr-xr-x 2 1000 1000 4.0K Jul 10 10:32 lib64  

bash-5.0# cp -r bin copy_bin  
bash-5.0# ls -lsh  
total 16K  
4.0K drwxr-xr-x 2    0    0 4.0K Jul 11 11:44 bin  
4.0K drwxr-xr-x 2    0    0 4.0K Jul 11 11:46 copy_bin  
4.0K drwxr-xr-x 3 1000 1000 4.0K Jul 10 10:34 lib  
4.0K drwxr-xr-x 2 1000 1000 4.0K Jul 10 10:32 lib64  

bash-5.0# du -sh .  
7.6M    .  
bash-5.0#  

bash-5.0# exit  
exit  
root@deb2:/home/deployer/isolate#  

```
