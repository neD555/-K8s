### Домашнее задание к занятию «Хранение в K8s»
### Задание 1. Volume: обмен данными между контейнерами в поде.

Задача.

Создать Deployment приложения, состоящего из двух контейнеров, обменивающихся данными.
### Шаги выполнения:
1.Создать Deployment приложения, состоящего из контейнеров busybox и multitool.

2.Настроить busybox на запись данных каждые 5 секунд в некий файл в общей директории.

3.Обеспечить возможность чтения файла контейнером multitool.
### Что сдать на проверку.
Манифесты:

containers-data-exchange.yaml.

Скриншоты:

Описание пода с контейнерами (kubectl describe pods data-exchange)

Вывод команды чтения файла (tail -f <имя общего файла>)

### Ответ.
<img width="644" height="859" alt="дз1(1)" src="https://github.com/user-attachments/assets/9f6460d0-57d3-4df4-b14a-47c1b0b3a037" />
<img width="525" height="264" alt="дз1(2)" src="https://github.com/user-attachments/assets/7abfa882-07ff-410a-8a31-00e071eb89a5" />

### Задание 2. PV, PVC.
Создать Deployment приложения, использующего локальный PV, созданный вручную.

Шаги выполнения:

1.Создать Deployment приложения, состоящего из контейнеров busybox и multitool, использующего созданный ранее PVC

2.Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.

3.Продемонстрировать, что контейнер multitool может читать данные из файла в смонтированной директории, в который busybox записывает данные каждые 5 секунд.

4.Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему. (Используйте команду kubectl describe pv).

5.Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV. Продемонстрировать, что произошло с файлом после удаления PV. Пояснить, почему.
### Что сдать на проверку.
Манифесты:

pv-pvc.yaml

Скриншоты:

Каждый шаг выполнения задания, начиная с шага 2.

Описания:

Объяснение наблюдаемого поведения ресурсов в двух последних шагах.

### Ответ.

<img width="522" height="126" alt="дз2(1)" src="https://github.com/user-attachments/assets/452770c5-b482-483c-9fa9-35d44bf75350" />
<img width="524" height="513" alt="дз2(2)" src="https://github.com/user-attachments/assets/737c33f8-c617-414c-8d45-6eb5992ec068" />
<img width="525" height="340" alt="дз2(3)" src="https://github.com/user-attachments/assets/0016ec57-ec14-4ae2-b709-9346e22a26e0" />
<img width="524" height="237" alt="дз2(4)" src="https://github.com/user-attachments/assets/10598aa7-1bf5-42d1-8b4d-5d5ccffe2295" />
<img width="523" height="699" alt="дз2(5)" src="https://github.com/user-attachments/assets/5d350a80-3927-41ad-b49a-16ed924d0512" />
<img width="528" height="422" alt="дз2(6)" src="https://github.com/user-attachments/assets/fdc56e18-1d93-46f8-9179-1bf781ef24aa" />
<img width="519" height="739" alt="дз2(7)" src="https://github.com/user-attachments/assets/bf893bef-b260-4cfb-af6f-76a23f776f7b" />
<img width="524" height="292" alt="дз2(8)" src="https://github.com/user-attachments/assets/b4e396f5-7f08-4fe3-8cbd-43f804352c8b" />

1.Почему после удаления Deployment и PVC PV стал Released.

После удаления PVC ресурс PV не удалился, а перешёл в состояние Released, потому что для него была указана политика persistentVolumeReclaimPolicy: Retain. Политика Retain означает, что
Kubernetes сохраняет том и данные на нём даже после удаления PersistentVolumeClaim.

2.Почему после удаления PV файл остался на локальном диске.

После удаления PV файл data.txt остался в директории /data/k8s/pv-task2, потому что использовался том типа hostPath. В случае hostPath Kubernetes удаляет только объект PV из своего
API, но не удаляет автоматически директорию и файлы на локальной файловой системе ноды.

### Задание 3. StorageClass.
Задача.

Создать Deployment приложения, использующего PVC, созданный на основе StorageClass.

Шаги выполнения:

1.Создать Deployment приложения, состоящего из контейнеров busybox и multitool, использующего созданный ранее PVC.

2.Создать SC и PVC для подключения папки на локальной ноде, которая будет использована в поде.

3.Продемонстрировать, что контейнер multitool может читать данные из файла в смонтированной директории, в который busybox записывает данные каждые 5 секунд.

Что сдать на проверку.

Манифесты:

 sc.yaml

Скриншоты:

 Каждый шаг выполнения задания, начиная с шага 2.

 ### Ответ.

 










