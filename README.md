# OAI 5G
##OAI 5G - ARM64 Setup instructions
---
#### Sources - 
1. Configure sources
   `
   sudo dpkg --add-architecture arm64
   echo -e \
        "deb [arch=arm64] https://mirror.enzu.com/ubuntu/  jammy main restricted\n"\
        "deb [arch=arm64] https://mirror.enzu.com/ubuntu/  jammy-updates main restricted\n"\
        "deb [arch=arm64] https://mirror.enzu.com/ubuntu/  jammy universe\n"\
        "deb [arch=arm64] https://mirror.enzu.com/ubuntu/  jammy-updates universe\n"\
        "deb [arch=arm64] https://mirror.enzu.com/ubuntu/  jammy multiverse\n"\
        "deb [arch=arm64] https://mirror.enzu.com/ubuntu/  jammy-updates multiverse\n"\
        "deb [arch=arm64] https://mirror.enzu.com/ubuntu/  jammy-backports main restricted universe multiverse"\
    | sudo tee /etc/apt/sources.list.d/arm-cross-compile-sources.list

  sudo cp /etc/apt/sources.list "/etc/apt/sources.list.`date`.backup"
  sudo sed -i -E "s/(deb)\ (http:.+)/\1\ [arch=amd64]\ \2/" /etc/apt/sources.list


   `
