# QC and Trimming
## Step 1 建立資料夾
```
cd /work/username
mkdir -p NGS_final/{metadata,log,script,result}
```
- metadata: 存放sample及run的list
- log: 存放out.log和err.log
- script: 存放code
- result: 存放所有分析的output

## Step 2 將要跑的run建立成list
1. 進入metadatay資料夾，輸入 ```cd NGS_final/metadata```
2. 建立run list
- 建立 AML run list  \
(1) 輸入 ```vim GSE49642_run.txt```  \
(2) 按鍵盤 <kbd>i</kbd> 進入編輯模式(底下會出現"-- INSERT --")  \
(3) 輸入共用excel的[RAW_DATA_DIR](https://docs.google.com/spreadsheets/d/1VJcEVEgGJvda-r6tbbAenRCqBA_cSyHO/edit?gid=1408776603#gid=1408776603)配分配到的5個 **run ID**
![螢幕擷取畫面 2026-05-18 111653](https://hackmd.io/_uploads/H1B6N-dJfg.png)
(4) 按 <kbd>Esc</kbd> 離開編輯模式
(5) 輸入 `:wq` 並按下 <kbd>Enter</kbd> 可儲存結果  
**❗若出現 "E45: 'readonly' option is set (add ! to override)" 的話，請輸入`:wq!`來儲存）❗**
- 建立 Normal run list  \
(1) 輸入 ```vim GSE111085_run.txt```  \
(2) 按鍵盤 <kbd>i</kbd> 進入編輯模式(底下會出現"-- INSERT --")  \
(3) 輸入共用excel的[RAW_DATA_DIR](https://docs.google.com/spreadsheets/d/1VJcEVEgGJvda-r6tbbAenRCqBA_cSyHO/edit?gid=1408776603#gid=1408776603)配分配到的5個 **run ID**
![螢幕擷取畫面 2026-05-18 111821](https://hackmd.io/_uploads/Sk7mBbOyzl.png)
(4) 按 <kbd>Esc</kbd> 離開編輯模式
(5) 輸入 `:wq` 並按下 <kbd>Enter</kbd> 可儲存結果  
**❗若出現 "E45: 'readonly' option is set (add ! to override)" 的話，請輸入`:wq!`來儲存）❗**

## Step 3 下載並修改要使用的script
1. 進入script資料夾，輸入
```
cd ../
cd script
```
2. 複製```01_AML_fastp.sh```和```01_Normal_fastp.sh```到script資料夾中
```
rsync -avz /work/evelyn92/NGS_final/script/01_AML_fastp.sh ./
rsync -avz /work/evelyn92/NGS_final/script/01_Normal_fastp.sh ./
```
3. 修改```username```
- 修改```AML_fastp.sh```  \
(1) 輸入 ```vim AML_fastp.sh```  \
(2) 按鍵盤 <kbd>i</kbd> 進入編輯模式(底下會出現"-- INSERT --")  \
(3) 將SLUM的```username```改成自己的國網帳號    
![螢幕擷取畫面 2026-05-18 114825](https://hackmd.io/_uploads/B19Ph-dkMe.png)  \
(4) 將```user1=username```的```username```改成自己的國網帳號    
![螢幕擷取畫面 2026-05-18 113717](https://hackmd.io/_uploads/B1E9KWdkfg.png)  \
(5) 按 <kbd>Esc</kbd> 離開編輯模式
(6) 輸入 `:wq` 並按下 <kbd>Enter</kbd> 可儲存結果  
**❗若出現 "E45: 'readonly' option is set (add ! to override)" 的話，請輸入`:wq!`來儲存）❗**
- 修改```Normal_fastp.sh```  \
(1) 輸入 ```vim Normal_fastp.sh```  \
(2) 按鍵盤 <kbd>i</kbd> 進入編輯模式(底下會出現"-- INSERT --")  \
(3) 將SLUM的```username```改成自己的國網帳號    
![截圖 2026-05-21 上午10.24.07](https://hackmd.io/_uploads/SJEMp13JMx.png)  \
(4) 將```user1=username```的```username```改成自己的國網帳號
![螢幕擷取畫面 2026-05-18 113629](https://hackmd.io/_uploads/S1vyq-OkMe.png)  \
(5) 按 <kbd>Esc</kbd> 離開編輯模式
(6) 輸入 `:wq` 並按下 <kbd>Enter</kbd> 可儲存結果  
**❗若出現 "E45: 'readonly' option is set (add ! to override)" 的話，請輸入`:wq!`來儲存）❗**

## Step 4 執行FastP
1. 輸入以下指令，來以sbatch job的方式送出編輯完成的草稿
```
sbatch 01_AML_fastp.sh
sbatch 01_Normal_fastp.sh
```
2. 若送出成功將會出現以下文字(結果在result資料夾已經指定好路徑)
```
Submitted batch job ＿＿＿
```

3. 可使用以下指令查看工作執行情況
```
sacct
```

## Step 5 檢查output
1. 進入存放AML fastp result的資料夾
```
cd ../
cd result
ls
```
2. 進入```fastp_run```子資料夾查看output
```
cd fastp_run
ls
```
- 跑完FasTP後每個run各會有4個檔案
![image](https://hackmd.io/_uploads/S1t0xM_Jzl.png)

## Step 6 建立clean FASTQ metadata，並將clean.fastq.gz檔案路徑記錄到[FastP_DIR](https://docs.google.com/spreadsheets/d/1VJcEVEgGJvda-r6tbbAenRCqBA_cSyHO/edit?gid=1618081040#gid=1618081040)
1. 下載建立`clean_fastp.tsv`的script
```
cd /work/username/NGS_fianl/script
rsync -avz /work/evelyn92/NGS_final/result/QC/Normal
/work/evelyn92/NGS_final/script/02_clean_fastq_metadata.sh ./
```
2. 執行```02_clean_fastq_metadata.sh```
```
bash 02_clean_fastq_metadata.sh username
```
3. 顯示檔案路徑
```
find /work/username/NGS_final/result/QC/AML -type f -name "*.fastq.gz"
find /work/username/NGS_final/result/QC/Normal -type f -name "*.fastq.gz"
```
4. 將路徑複製貼到[FastP_DIR](https://docs.google.com/spreadsheets/d/1VJcEVEgGJvda-r6tbbAenRCqBA_cSyHO/edit?gid=1618081040#gid=1618081040)

## Step 7 開放檔案權限
1. 讓特定user可以讀取及修改
> userA~B:要開放權限給該位user的國網帳號
> username:自己的國網帳號
```
setfacl -R -m u:userA:rwX /work/username/NGS_final
setfacl -R -m u:userB:rwX /work/username/NGS_final
setfacl -R -m u:userC:rwX /work/username/NGS_final
setfacl -R -m d:u:userA:rwX /work/evelyn92/NGS_final
setfacl -R -m d:u:userB:rwX /work/evelyn92/NGS_final
setfacl -R -m d:u:userC:rwX /work/evelyn92/NGS_final
```
> 成員的國網帳號
> 1) 王嘉嬣:b10404008
> 2) 張文綺:evelyn92
> 3) 何亮宏:austinhe19
> 4) 黃子霆:r14943020

2. 確認權限開放成功
```
getfacl /work/username/NGS_final
```
![螢幕擷取畫面 2026-05-18 124808](https://hackmd.io/_uploads/H1WE5fu1zx.png)

