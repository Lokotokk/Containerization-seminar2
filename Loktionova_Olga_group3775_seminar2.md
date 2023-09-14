# Урок 2. Механизмы контрольных групп  
1) запустить контейнер с ubuntu, используя механизм LXC  
2) ограничить контейнер 256 Мб ОЗУ и проверить, что ограничение работает    

*Задание по желанию ..*    
3) добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер действительно запустился самостоятельно  

1. Cоздаем контейнер:  
   `lxc-create -n hmseminar2 -t ubuntu`
   
    ![](https://github.com/Lokotokk/Containerization-seminar2/blob/main/images/create.png) 

   Запуск:  
   `lxc-start -n hmseminar2`  
   Вход:  
   `lxc-attach -n hmseminar2`  
   Проверка памяти:  
   `free -m` —проверяем пямаять
   Выход:  
   `exit`  
   Закрываем:  
   `lxc-stop -n hmseminar2`
 
   ![](https://github.com/Lokotokk/Containerization-seminar2/blob/main/images/start.png)
   
3. Открываем конфигурационный файл:  
   `nano /var/lib/lxc/hmseminar1/config`  
   
    ![](https://github.com/Lokotokk/Containerization-seminar2/blob/main/images/memory.png)  
 
   Добавляем настройку(ограничение памяти):  
      `lxc.cgroup2.memory.max = 256M`  

   ![](https://github.com/Lokotokk/Containerization-seminar2/blob/main/images/memory1.png)   
   
   Проверяем, что ограничение работает:  
      `lxc-start -n hmseminar2`  
      `lxc-attach -n hmseminar2`  
      `free -m`  
      `exit`  
      `lxc-stop -n hmseminar2`

  ![](https://github.com/Lokotokk/Containerization-seminar2/blob/main/images/memory3.png)  
   
   
 5. Открываем конфигурационный файл:  
   `nano /var/lib/lxc/hmseminar1/config`

    Добавляем автозапуск:
    
    `lxc.start.auto  =  1`   
    `lxc.start.delay = 15`   
    `lxc.start.order = 50`  

      ![](https://github.com/Lokotokk/Containerization-seminar2/blob/main/images/autostart.png)  
      ![](https://github.com/Lokotokk/Containerization-seminar2/blob/main/images/autostart1.png)
