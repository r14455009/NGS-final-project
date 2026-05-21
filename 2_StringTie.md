# Expression quantification

## Step 1 建立 sample BAM list
1. 建立list
```
find /work/username/NGS_final/result/ALN -name "*.sorted.bam" | sort > /work/username/NGS_final/result/ALN/bam.list
```
2. 檢查list
```
cat /work/evelyn92/NGS_final/result/ALN/bam.list
```
## Step 2 下載並修改要使用的script
1. 進入script資料夾，輸入`cd /work/username/NGS_final/script`
2. 複製```04_stringtie.sh```到script資料夾中
```
rsync -avz /work/evelyn92/NGS_final/script/04_stringtie.sh ./
```
3. 修改```username```  \
(1) 輸入 ```vim 04_stringtie.sh```  \
(2) 按鍵盤 <kbd>i</kbd> 進入編輯模式(底下會出現"-- INSERT --")  \
(3) 將SLUM的```username```改成自己的國網帳號  \
![截圖 2026-05-21 下午5.00.46](https://hackmd.io/_uploads/rycY9HnyGg.png)  \
(4) 將```user=username```的```username```改成自己的國網帳號  \
![截圖 2026-05-21 下午5.01.29](https://hackmd.io/_uploads/r1us5B21Mx.png)  \
(5) 按 <kbd>Esc</kbd> 離開編輯模式  \
(6) 輸入 `:wq` 並按下 <kbd>Enter</kbd> 可儲存結果  \
**❗若出現 "E45: 'readonly' option is set (add ! to override)" 的話，請輸入`:wq!`來儲存）❗**

# Step 3 執行 StringTie
1. 輸入以下指令，來以sbatch job的方式送出編輯完成的草稿
```
sbatch 04_stringtie.sh
```
2. 若送出成功將會出現以下文字(結果在result資料夾已經指定好路徑)
```
Submitted batch job ＿＿＿
```

3. 可使用以下指令查看工作執行情況
```
sacct
```

## Step 4 檢查output
1. 進入存放AML tringtie result的資料夾
```
cd ../
cd result/stringtie
```
2. 進入```run```子資料夾查看output
```
cd run
ls
```
- 跑完FasTP後每個run各會有7個檔案
![截圖 2026-05-21 下午5.10.54](https://hackmd.io/_uploads/HJWrnrn1fx.png)

## Step 5 將.gtf檔案路徑記錄到[StringTie_DIR](https://docs.google.com/spreadsheets/d/1VJcEVEgGJvda-r6tbbAenRCqBA_cSyHO/edit?gid=382352135#gid=382352135)
1. 顯示檔案路徑
```
find /work/username/NGS_final/result/stringtie/AML -type f -name "*.gtf"
find /work/username/NGS_final/result/stringtie/Normal -type f -name "*.gtf"
```
2. 將路徑複製貼到[StringTie_DIR](https://docs.google.com/spreadsheets/d/1VJcEVEgGJvda-r6tbbAenRCqBA_cSyHO/edit?gid=382352135#gid=382352135)
