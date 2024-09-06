# 111 大學部OS - HW1 demo 測資與參考答案

**[[demo.txt下載連結]](https://drive.google.com/file/d/1lYklWizGoZtPCjDQ-otDPdwBiRIexmPr/view?usp=sharing)**

## part 1

### test simple command

test case: ``cat demo.txt``
expected result:

```text
Today is os' day.
I am a student in CSIE. 
I love os, you love os, David loves os.
The hw-demo will take place in oslab.
I am going to try my best.
Have a nice os' day. 
```

### test background execution

test case: ``cat demo.txt &``
expected result: (pid 數字可能不同)

```text
[Pid]: 123
Today is os' day.
I am a student in CSIE. 
I love os, you love os, David loves os.
The hw-demo will take place in oslab.
I am going to try my best.
Have a nice os' day. 
```

### test input re-direction

test case: ``cat < demo.txt``
expected result:

```text
Today is os' day.
I am a student in CSIE. 
I love os, you love os, David loves os.
The hw-demo will take place in oslab.
I am going to try my best.
Have a nice os' day. 
```

### test output re-direction

test case: ``cat demo.txt > out1`` 然後 ``cat out1``
expected result:

```text
Today is os' day.
I am a student in CSIE. 
I love os, you love os, David loves os.
The hw-demo will take place in oslab.
I am going to try my best.
Have a nice os' day. 
```

### test input/output re-direction

test case: ``cat < demo.txt > out2`` 然後 `` $ cat out2 ``
expected result:

```text
Today is os' day.
I am a student in CSIE. 
I love os, you love os, David loves os.
The hw-demo will take place in oslab.
I am going to try my best.
Have a nice os' day. 
```

### test pipe

test case: ``cat demo.txt | tail -2``
expected result:

```text
I am going to try my best.
Have a nice os' day.
```

### test pipe again

test case:``cat demo.txt | grep os``
expected result:

```text
Today is os' Day.
I love os, you love os, David loves os.
The hw-demo will take place in oslab.
Have a nice os' day
```

### test multi-pipe

test case:``cat demo.txt | tail -5 | head -3 | grep os``
expected result:

```text
I love os, you love os, David loves os.
The hw-demo will take place in oslab.
```

### test multi-pipe + input/output re-direction

test case:``cat < demo.txt | tail -5 | head -3 | grep os > out3`` 然後 ``cat out3``
expected result:

```text
I love os, you love os, David loves os.
The hw-demo will take place in oslab.
```

### test multi-pipe + input/output re-direction + background execution

test case:``cat < demo.txt | tail -5 | head -3 | grep os > out4 &`` 然後 ``cat out4``
expected result:

```text
[Pid]: 321 (應跟前面的 123 不同)
和
I love os, you love os, David loves os.
The hw-demo will take place in oslab.
```

## part 2

### test echo

``echo (隨便一串英文數字)`` (顯示和餵給echo相同的英文數字)
``echo (隨便另一串英文數字)`` (顯示和餵給echo相同的英文數字)
``echo -n 123`` (顯示 123 且沒換行)
``echo -n -n -n`` (沒換行，並顯示兩個 -n)
``echo 321`` (顯示 321 且有換行)
``echo --version`` (應該只會看到 --version)

#### test record and replay

``record`` (record 要有最近打過的16個指令的正確紀錄，並且最新的(數字16)應要是 record)

``replay [number]`` (挑一個你重現的指令, 看輸出對不對)

``replay [number] | head -1``  (挑一個你重現的指令, 看輸出對不對)

``record`` (看一下 record 顯示的數字有沒有對應更新)

``replay [number] | head -1 > out5`` (挑一個你重現的指令)

``cat out5`` (看內容對不對)

#### test mypid

``mypid -i``
``mypid -p 前一道指令的輸出數字``
``mypid -c 前一道指令的輸出數字`` (注意有沒有對應的pid, 即第一行 mypid -i 的輸出)
``mypid -c 1`` (應該要顯示很多個 pid 數字)
