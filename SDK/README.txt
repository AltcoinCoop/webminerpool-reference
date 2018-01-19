WEBMINERPOOL.COM SDK - VERSION: JANUARY 7th, 2018
--------------------------------------------------

How to use the website
----------------------

Mining the cryptocurrency AEON is also supported:

https://webminerpool.com/aeon

URL Parameters example:

https://webminerpool.com?pool=minexmr.com&address=
422QQNhnhX8h(..)&threads=4&password=secret&autostart=true&throttle=50

- Note that "pool" has to be a registered pool at the webminerpool.com server,
  i.e. setting the pool to some unknown value will fail.

- Address should be set to a valid XMR address.

- Threads should not be set (much) higher than the number of CPU cores on the 
  computer mining. Otherwise the total hashrate will suffer. You can use "-1" for
  a automatic configuration of this value.

- Password is the pool password. For all servers registered at webminerpool.com this
  can be left empty. Most pools use this value to distinguish different workers.

- If autostart is set to true the mining process will start after opening the page.

- Throttle sets the default throttling value.


SDK content description
-----------------------

There are folders for Monero (xmr) and Aeon (aeon) 

lvl1, lvl2 and lvl3 all contain the same mining example.

- lvl3 contains the complete set of miner scripts 
  - miner.js   the main miner file
  - worker.js  a webworker doing the work
  - cn.js      a wrapped webassembly file for calculating hashes

- lvl2 contains one file. All of SDK3 files wrapped into one file "miner.js".

- lvl1 contains no additional scripting files. The scripting file is hosted
  on webminerpool.com

IF you want to add a miner to your own website, use lvl2 (best) or
lvl1. lvl3 is good for reference or for users creating their own miner
logic.

Some browsers (Firefox at the moment) do allow you to run the scripts locally
on your computer. If this does not work host the samples somewhere (Chrome).


Adding a miner to your webpage
------------------------------

You need to add

<script src="https://www.webminerpool.com/miner.js"></script>

to your own page (better: also upload miner.js on your own page) and
call for example

startMining("moneroocean.stream", "422QQNhnhX8hmMEkF3TWePWSvKm6DiV7sS3Za2dXrynsJ1w8U6AzwjEdnewdhmP3CDaqvaS6BjEjGMK9mnumtufvLmz5HJi");


The startMining function can take additional arguments

startMining(pool,
        address, password, numThreads, userid);

- pool        , this has to be a pool available at webminerpool.com.
- address     , a valid XMR address you want to mine to.
- password    , password for your pool. Often not needed.
- numThreads  , the number of threads the miner uses. Use "-1" for auto-config.
- userid      , allows you to identify the number of hashes calculated by a user. 
		see getuserstats in "other" folder.

To throttle the miner just use the global variable "throttleMiner", e.g. 
   ~~~~~~~~

startMining("moneroocean.stream",
        "422QQNhnhX8hmMEkF3TWePWSvKm6DiV7sS3Za2dXrynsJ1w8U6AzwjEdnewdhmP3CDaqvaS6BjEjGMK9mnumtufvLmz5HJi");

throttleMiner = 20;

throttleMiner -> percentage of miner throttling. If you set this to 20, the
                 cpu workload will be approx. 80% (for 1 thread / CPU).
                 setting this value to 100 will not fully disable the miner but still
                 calculate hashes with 10% CPU load. See worker.js for details.


If you do not want to show the user your address or even the password you have to create 
a "loginid". With the loginid you can start mining with

startMiningWithId(loginid)

or with optional input parameters:

startMiningWithId(loginid, numThreads, userid)

Get a loginid by opening "register.html" in the "other" folder. In the "other" folder
you also find a script which enumerates all available pools and a script which shows
you the amount of hashes calculated by a userid.


I like shitcoins, how do I mine ..
----------------------

SUMO 

https://webminerpool.com?pool=SUMO_sumokoin.com

ETN

https://webminerpool.com?pool=ETN_poolmining.org

Other pools can be added on request.


