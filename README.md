# piphonom_infra
piphonom Infra repository

************

bastion_IP = 35.210.212.166
someinternalhost_IP = 10.132.0.3

************

testapp_IP = 104.155.83.151
testapp_port = 9292

************

В простом случае startup_script объединяет содержимое всех bash скриптов.

Для выполнения startup_script.sh в момент создания инстанса нужно добавить
опцию --metadata-from-file startup-script=/path/to/file:

gcloud compute instances create reddit-app-2  --boot-disk-size=10GB \
--image-family ubuntu-1604-lts --image-project=ubuntu-os-cloud \
--machine-type=g1-small --tags puma-server --restart-on-failure \
--metadata-from-file startup-script=./startup-script.sh

------------

Для создания правила файерволла через gcloud нужно выполнить:

gcloud compute firewall-rules create default-puma-server --allow tcp:9292 \
--direction INGRESS --source-ranges "0.0.0.0/0" --target-tags "puma-server" \
--priority 1000

************
