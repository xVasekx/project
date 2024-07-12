Запуск playbook для определенного хоста
ansible-playbook playbook.yml -l hostname


восстановление masterdb.
ansible-playbook playbook.yml -l masterdb
ansible-playbook mysql_replication/tasks/restore_master.yml

Возобновление репликации.
на мастере:
show master status\G

на слейве:
SHOW SLAVE STATUS\G
stop slave;
STOP REPLICA IO_THREAD FOR CHANNEL '';
CHANGE MASTER TO master_auto_position=0;
change master to MASTER_LOG_FILE='Relay_Master_Log_File', Master_Log_Pos=Relay_Log_Pos;
change master to MASTER_LOG_FILE='Master_Log_File', Master_Log_Pos=Read_Master_Log_Pos;
SHOW SLAVE STATUS\G


