

# 1. 换源（可选但推荐）

先使用小鱼的一键脚本更换系统源（推荐ustc）和python源
```
wget http://fishros.com/install -O fishros && bash fishros
```



# 2.安装openvino

### 方法一 ：通过APT安装（我用的是方法二）

```
wget https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB 

sudo apt-key add GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB

echo "deb https://apt.repos.intel.com/openvino/2024 ubuntu22 main" | sudo tee /etc/apt/sources.list.d/intel-openvino-2024.list

sudo apt update

apt-cache search openvino

sudo apt install openvino-2024.6.0
```

### 方法二：通过Archive安装

```
sudo mkdir /opt/intel

cd <user_home>/Downloads

curl -L https://storage.openvinotoolkit.org/repositories/openvino/packages/2024.6/linux/l_openvino_toolkit_ubuntu22_2024.6.0.17404.4c0f47d2335_x86_64.tgz --output openvino_2024.6.0.tgz
tar -xf openvino_2024.6.0.tgz
sudo mv l_openvino_toolkit_ubuntu22_2024.6.0.17404.4c0f47d2335_x86_64 /opt/intel/openvino_2024.6.0

cd /opt/intel/openvino_2024.6.0
sudo -E ./install_dependencies/install_openvino_dependencies.sh



cd /opt/intel

sudo ln -s openvino_2024.6.0 openvino_2024

source /opt/intel/openvino_2024/setupvars.sh
```  
建议在  ~/.bashrc  文件中添加下面的命令，这样就不用每次开启终端时都source了：
```
source /opt/intel/openvino_2024/setupvars.sh
```

# 3. conda创建YOLO虚拟环境（没安装Anaconda的需要先安装）

```
conda create -n yolo python=3.10
```

# 4. 开始配置yolo环境

```
conda activate yolo

pip install -U ultralytics

pip3 install torch torchvision --index-url https://download.pytorch.org/whl/cu130
```

到此为止，YOLO的环境与Openvino的环境应该都已经配置完毕了。