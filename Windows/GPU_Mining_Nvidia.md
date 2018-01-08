# GPU Mining for GRLC (Windows)

#### Note: This guide only works for Nvidea GPUs

### Big thanks to @Pandawan#4158 over on discord for writing this guide!


## Introduction

This guide will show you step by step how to mine garlicoin on windows machines using an Nvidea GPU. While the current chain is only TestNet, it still provides valuable network testing and gets you used to mining for when the MainNet goes live.

Feel free to submit a PR if you feel like there are any changes that should be made to this guide.

# Table of Contents
1. [Pool Mining](#Pool-Mining)
2. [Solo Mining](#Solo-Mining)
3. [Solo vs. Pool](#Solo-vs.-Pool)
4. [How Pool Mining works](#How-Pool-Mining-Works)
5. [Credits Donate](#Credits-Donate)

Quick Links:

GarlicBread Explorer (see transactions�): [http://explorer.garlicoin.io/](http://explorer.garlicoin.io/)

Pool Mining GUI: [http://5.196.13.45/index.php?page=statistics&action=pool](http://5.196.13.45/index.php?page=statistics&action=pool)

Pool Mining Stats: [http://5.196.13.45:4000/api/pools/grlc1/miner/YOUR_ADDRESS_HERE/stats](http://5.196.13.45:4000/api/pools/grlc1/miner/YOUR_ADDRESS_HERE/stat)

Pool Stats: [http://5.196.13.45:4000/api/pools/grlc1/](http://5.196.13.45:4000/api/pools/grlc1/)

Pool Blocks: [http://5.196.13.45:4000/api/pools/grlc1/blocks](http://5.196.13.45:4000/api/pools/grlc1/blocks)



## Pool Mining

This uses `@Vilsol#2060�s` mining pool.

### Step 0: Prerequisites
Make sure you have a CUDA compatible GPU. This should work with most modern GPUs. (Anything in the 9 or 10 series is 100% going to work). Also make sure you have updated your Nvidia drivers.

### Step 1: Set up the basic Garlic Miner/Wallet
First you want to follow [this guide](https://github.com/brennanmcdonald/github-bible/) so you can have a wallet running. Make sure you keep the 
```
garlicoind -testnet -connect=52.89.91.13 
```
Command Prompt window opened and connected.

### Step 2: Setting up ccminer
Download ccminer from the github repo [here](https://github.com/tpruvot/ccminer/releases). 

If you have a 64bit machine (you probably shouldn�t mine on 32bit anyways), then download the [ccminer-x64-2.2.4-cuda9.7z](https://github.com/tpruvot/ccminer/releases/download/2.2.4-tpruvot/ccminer-x64-2.2.4-cuda9.7z) file. Otherwise, download the [ccminer-x86-2.2.4-cuda9.7z](https://github.com/tpruvot/ccminer/releases/download/2.2.4-tpruvot/ccminer-x86-2.2.4-cuda9.7z) file. Extract all those files into a new directory (location doesn�t matter). 

NOTE: Do not download from source or else you will have to compile the whole program yourself. This might take hours, just download the files above!

### Step 3: Creating a bat file
You will want to create a bat file with the commands to setup and start the GPU miner. 

Here�s how to do it. In the same folder, create a new ``RUN-GRLC.bat`` file (Right click > Create New > Text file > Rename it to RUN-GRLC.bat). Inside this file, you want to type this:
```
ccminer-x64 --algo=scrypt -o stratum+tcp://5.196.13.45:3042 -u {YOUR GARLICOIN ADDRESS HERE} -listen
Pause
```

![Creating a batch file](https://i.imgur.com/DbsVXu7.png)


You can change the address after the -u (change from {YOUR GARLICOIN ADDRESS HERE} to whatever your garlicoin address is). 

You can now save the file, and run it.

NOTE: It might take a while to load before it actually starts mining. If you are stuck on something like this, just wait. It should take between 1-15 mins.

### Step 4: Enjoy! 
Run the file and you should be good to go! If you have any issues you can contact me on discord @Pandawan#4158

### Step 5: Extra info

If you want to stop the process, just press Ctrl + C (when you are in the command prompt window). This should ask if you want to quit, then type y (and press enter).


Also, you can check your pool stats (# of shares, total paid, hashrate�) here

[http://5.196.13.45:4000/api/pools/grlc1/miner/YOUR_ADDRESS_HERE/stats](http://5.196.13.45:4000/api/pools/grlc1/miner/YOUR_ADDRESS_HERE/stats)

(Just replace the YOUR ADDRESS HERE to whatever your address is)

### Troubleshooting:
If it doesn�t work, try removing the -listen from the ``RUN-GRLC.bat`` file. This might not fix it, but it�s worth a try. If you get strange errors, first try restarting both command prompts. (Both the ``garlicoind -testnet -connect=52.89.91.13`` command, and the GPU mining command).


## Setting up Miner for Solo
This hasn�t fully been tested, but I guess you could try. 
For now, solo mining is worth it because the difficulty is very low. But once it goes up, solo mining will be next to impossible. 

### Step 1: Downloading ccminer for Solo
Download ccminer here, this is a different version which works with solo mining. Extract everything from the zip file.



### Step 2: Creating a bat file
Create a new one called ``RUN-SOLO-GRLC.bat.`` Inside you want to put this 
ccminer.exe --algo=scrypt -o 127.0.0.1:42070 -u test -p test --no-longpoll --no-getwork --no-stratum --coinbase-addr=mtWqkNC3szbAjwrmcHjbcTzTsyUcjriCQj -listen
pause

And replace the address (mtWqkNC3szbAjwrmcHjbcTzTsyUcjriCQj), to your own. 

### Step 3: Running
This should be enough to get you started. Running the RUN-SOLO-GRCL.bat should start mining. This is a bit different from pool mining in that every time you see �Accepted .. yes!� it means that you have actually mined a block rather than gained a share.


Thanks to @SirFish#7124 and @Equinox Fox#5914 for the Solo Mining info!

## Solo vs. Pool
Solo mining is when you mine by yourself, all your efforts go towards creating a block. This is very efficient when the difficulty is low (when a coin just started) because finding blocks is easy. You can get 50 coins every time you mine one block. 

Pool mining is when you mine along with other miners as a group. You connect to that pool rather than the network itself, and all your hashes go to that pool. That pool will get the 50 coins, and then distributes them all based on how much each miner has contributed/mined. The more you help mining, the more you get. Pool mining is much more efficient when the difficulty is high because pools can mine much faster in total (add up all the miners in the pool). So the pool will have mined blocks before the solo miners are done. (In which case, pool mining is more profitable since you are more likely to mine blocks).

## How Pool Mining works
Ok guys, so basically here's how this works:
If you mine in a pool, you get a share every time it says "accepted ... yes!"
The pool gets payed from the blocks that everybody mines. In this payout, the pool gets 50 GRLC, and distributes it to everybody based on how many shares they own.
These payouts happen 100 blocks after the block that you have mined. 
You can close the miner and your shares are still there, you just need to wait for 100 mined blocks.

If you had been there when we mined 16778 you would get payout at 16878

TLDR: If you�re mining in a pool and you�re not seeing your coins in your wallet, just wait a bit!
