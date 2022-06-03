# 运行手册
## 1. 下载项目
```bash
git clone https://github.com/zhangjenny/AutoDrive.git
```

## 2. 进入AutoDrive/Leaderboard
```bash
cd AutoDrive/leaderboard
sudo pip3 install -r requirements.txt
```

## 3. 创建模型checkpoint保存路径
```bash
cd ..
mkdir model_ckpt
wget https://s3.eu-central-1.amazonaws.com/avg-projects/transfuser/models.zip -P model_ckpt
unzip model_ckpt/models.zip -d model_ckpt/
rm model_ckpt/models.zip
```

## 4. 用root用户创建自己模型保存路径并复制预训练模型
```bash
sudo -s
mkdir ./model_ckpt/transfuser_newfusion
cp /content/drive/MyDrive/Auto-Drive/transfuser-newfusion/log/transfuser-newfusion/best_model.pth ./model_ckpt/transfuser_newfusion/best_model.pth
mkdir ./model_ckpt/transfuser_convnext
cp /content/drive/MyDrive/Auto-Drive/transfuser-convnext/log/transfuser-convnext/best_model.pth ./model_ckpt/transfuser_convnext/best_model.pth
mkdir ./model_ckpt/transfuser_cross
cp /content/drive/MyDrive/Auto-Drive/transfuser-z/log/transfuser-z/best_model.pth ./model_ckpt/transfuser_cross/best_model.pth
```
## 5. 给colab用户加777权限
```bash
cd ..
su colab
sudo chmod -R 777 AutoDrive/
cd AutoDrive
```

## 6. 安装Vim
```bash
sudo apt-get install vim
```

## 7. 修改leaderboard/scripts/run_evaluation.sh中的
```bash
vim leaderboard/scripts/run_evaluation.sh
```

需要修改的内容如下：
```bash
export TEAM_AGENT=leaderboard/team_code/transfuser_newfusion_agent.py
export TEAM_CONFIG=model_ckpt/transfuser_newfusion
export CHECKPOINT_ENDPOINT=results/newfusion_result.json
```

## 8. 运行脚本
```bash
CUDA_VISIBLE_DEVICES=0 ./leaderboard/scripts/run_evaluation.sh
```





