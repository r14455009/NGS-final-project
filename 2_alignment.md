# Alingment
## Step 1 下載並修改要使用的script
1. 進入script資料夾，輸入 `cd NGS_final/script`
2. 複製`03_hisat2.sh`到script資料夾中
```
rsync -avz /work/evelyn92/NGS_final/script/03_hisat2.sh ./
```
3. 修改username  \
(1) 輸入 vim 03_hisat2.sh  \
(2) 按鍵盤 <kbd>i</kbd> 進入編輯模式(底下會出現"-- INSERT --")  \
(3) 將SLUM的username改成自己的國網帳號  \
![螢幕擷取畫面 2026-05-18 171517](https://hackmd.io/_uploads/BJpAOUukMl.png)  \
(4) 將```user=username```的```username```改成自己的國網帳號  \   
![螢幕擷取畫面 2026-05-18 171658](https://hackmd.io/_uploads/rkYmKLdyzx.png)  \
(5) 按 <kbd>Esc</kbd> 離開編輯模式  \
(6) 輸入 `:wq` 並按下 <kbd>Enter</kbd> 可儲存結果  \
**❗若出現 "E45: 'readonly' option is set (add ! to override)" 的話，請輸入`:wq!`來儲存）❗**

## Step 4 執行HISAT2
1. 輸入以下指令，來以sbatch job的方式送出編輯完成的草稿
```
sbatch 03_hisat2.sh
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
1. 進入存放HISAT2 result的資料夾查看output
```
cd /work/username/NGS_final/result/ALN/AML
ls
```
2. 進入```run```子資料夾查看output
```
cd run
ls
```
- 跑完HISAT2後每個run各會有3個檔案  \
![image](https://hackmd.io/_uploads/HJR0Yqu1Mg.png)  

## Step 6 將sorted.bam檔案路徑記錄到[ALN_DIR](https://docs.google.com/spreadsheets/d/1VJcEVEgGJvda-r6tbbAenRCqBA_cSyHO/edit?gid=1530628311#gid=1530628311)
1. 顯示檔案路徑
```
find /work/username/NGS_final/result/ALN/AML -type f -name "*.sorted.bam"
find /work/username/NGS_final/result/ALN/Normal -type f -name "*.sorted.bam"
```
2. 將路徑複製貼到[ALN_DIR](https://docs.google.com/spreadsheets/d/1VJcEVEgGJvda-r6tbbAenRCqBA_cSyHO/edit?gid=1530628311#gid=1530628311)
