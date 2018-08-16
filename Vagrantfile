SWIFT_URL = 'https://swift.org/builds/swift-4.1.2-release/ubuntu1604/swift-4.1.2-RELEASE/swift-4.1.2-RELEASE-ubuntu16.04.tar.gz'.freeze
SWIFT_PATH = 'swift-4.1.2-RELEASE-ubuntu16.04'.freeze
ARCHIVE = 'swift.tar.gz'.freeze
USER_NAME = 'vagrant'.freeze
SWIFT_HOME = "/home/#{USER_NAME}/#{SWIFT_PATH}".freeze

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  
  config.vm.provision "shell", inline: <<-SHELL

  export DEBIAN_FRONTEND=noninteractive

  ## Install swift prerequisites
  echo "Installing prerequisites"
  sudo apt-get -qq update && sudo apt-get upgrade -y
  sudo apt-get install -y clang \
    libpython2.7
  
  ## Download Swift
  if [ ! -d "#{SWIFT_PATH}" ]; then
    echo "Downloading Swift"
    curl -s -o "#{ARCHIVE}" "#{SWIFT_URL}"

    ## Unpack archive
    tar zxf "#{ARCHIVE}"

    ## change swift file ownership
    chown -R "#{USER_NAME}" "#{SWIFT_PATH}"

    ## Remove archive
    rm "#{ARCHIVE}"
  fi
  
  ## Export Swift bin to PATH
  if [ $(grep -c "#{SWIFT_PATH}" .profile) -eq 0 ]; then
    echo "Adding swift to path"
    echo "export PATH="#{SWIFT_HOME}"/usr/bin:\"${PATH}\"" >> .profile
  fi
  
  echo "Swift finished install on Linux"
  SHELL
end
