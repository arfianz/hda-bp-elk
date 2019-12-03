# Logging Kubernetes Cluster denga ELK Stack
<br>
<br>Langkah pertama adalah membuat namespace untuk ELK-Stack, menggunakan perintah:
<br>$ kubectl create namespace bp-log
<br>
<br>Kemudian dilanjutkan dengan membuat statefullset untuk pod elasticsearch, dengan perintah:
<br>$ kubectl apply -f 01-elasticsearch-ss.yaml
<br>
<br>Langkah berikutnya adalah deploy logstash sebagai log forwarder, dengan perintah:
<br>$ kubectl apply -f 02-logstash-deployment.yaml
<br>
<br>Dilanjutkan dengan deploy log farmer (beat) yang terdiri dari filebeat dan metricbeat, dengan perintah
<br>$ kubectl apply -f 03-filebeat-ds.yaml
<br>$ kubectl apply -f 04-metricbeat-ds.yaml
<br>
<br>Selanjutnya adalah deploy kibana sebagai UI, dengan perintah:
<br>$ kubectl apply -f 05-kibana-deployment.yaml
<br>Untuk mengakses kibana, dapat dilihat di service dan lihat di endpoint
<br>
<br>Dikarenakan elasticsearch akan menyimpan semua data, dan lama kelamaan akan memakan space storage, maka dibuat cronjob dengan memanfaatkan modul curator dari elasticsearch.
<br>$ kubectl apply -f 06-curator-cronjob.yaml
