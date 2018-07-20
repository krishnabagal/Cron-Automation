# Cron-Automation

![alt tag](images/CronBuild.png "Imamge01")


```bash
├── cron
│   ├── roles
│   │   └── common
│   │       └── tasks
│   │           ├── cron.yml
│   │           └── main.yml
│   └── site.yml
```

```bash
:/etc/ansible:0:>> cat cron/site.yml 
---
  - hosts: cron
    become: yes
    become_user: root
    gather_facts: no
    roles:
       - common
```
```bash
:/etc/ansible:0:>> cat cron/roles/common/tasks/cron.yml
---
- cron:
    name: '{{ Name }}'
    minute: '{{ Minute }}'
    hour: '{{ Hours }}'
    day: '{{ Day }}'
    month: '{{ Month }}'
    weekday: '{{ DayOfWeek }}'
    job: '{{ Command }}'
    state: '{{ State }}'
    user: root
- service:
    name: cron
    enabled: yes
    state: restarted
```
```bash
:/etc/ansible:0:>> cat cron/roles/common/tasks/main.yml
---
 - include: cron.yml
```
```bash
sudo ansible-playbook -v /etc/ansible/cron/site.yml -l $Host -e Name="'$Name'" -e Minute="'$Minute'" -e Hours="'$Hours'" -e Day="'$Day'" -e Month="'$Month'" -e DayOfWeek="'$DayOfWeek'" -e Command="'$Command'" -e State="$State" 
```
