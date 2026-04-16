Vagrant.configure("2") do |config|
  # Используем официальный образ Ubuntu 22.04 LTS
  config.vm.box = "ubuntu/jammy64"

  # Настройка общей папки через RSync
  # "." – текущая папка на хосте, "/vagrant" – папка внутри ВМ
  config.vm.synced_folder ".", "/vagrant", type: "rsync",
    rsync__exclude: [".vagrant/", ".git/"]   # исключаем служебные папки

  # Провизия: выполняется один раз при создании ВМ
  config.vm.provision "shell", inline: <<-SHELL
    # Обновляем список пакетов и устанавливаем wget, если его нет
    apt-get update
    apt-get install -y wget
    # Скачивание файла в домашнюю папку пользователя vagrant
    wget -O /home/vagrant/downloaded_file.html https://example.com
    # Меняем владельца файла на vagrant
    chown vagrant:vagrant /home/vagrant/downloaded_file.html
  SHELL

  # Создание 3х виртуальных машин
  (1..3).each do |i|
    config.vm.define "ubuntu-vm#{i}" do |node|
      node.vm.hostname = "ubuntu-vm#{i}"
    end
  end
end