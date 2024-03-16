



Changes specific to DINGOCOIN
=====================================

1. Recommended config: dingocoin ready settings.json.template - default social images in footer (insert users, passwords, database name at the top).

2. Config with better social media images. Dingocoin ready settings.json.with_logos.template (insert users, passwords, database name at the top).
* Social images and configuration are ready to use. But light logos are in production version instead - a lawyer needed to confirm how to do it 100% legal and safe.

3. Added Discord, X, Github and Telegram footer images to public/img (please see 2.)

4. Added basic SEO meta data into the head: title, author and keywords. How-to add more meta data is described in settings.json as a comment.

5. Background of Richlist pie set to transparent, grid: {borderWidth:0, shadow:false, background:'transparent'} in views/richlist.pug

6. Dingocoin images everywhere

7. Dingocoin screenshots
 



Metadata "author" is "Various authors listed in file LICENSE (located on code root). Dingocoin specific settings added by Dingocoin Project.".
Think it's legal and correct.



Scripts
==================


Linux user that executes next scripts is to be unprivileged.


Start is to be executed at "init multuiser" time, rc.local style:

#!/bin/bash
	cd /home/user/E_iquidus/ &&
	rm -f /home/user/E_iquidus/tmp/* &&
	#screen -S Enpm -d -m /usr/bin/npm start # testing only
	# global npm, pm2 install path in next line
	/usr/bin/npm run prestart "pm2" && /usr/bin/pm2 start ./bin/instance -i 0 -n explorer -p "./tmp/pm2.pid" --node-args="--stack-size=10000"
exit 0



Stop is to be executed at "exit multiuser" time, rc.local-shutdown style. Controlled stop will enable write of all data to database before exit:

#!/bin/bash
	cd /home/user/E_iquidus/ &&
	/usr/bin/pm2 stop explorer
exit 0



update Top 100 sudo and regular version:

#!/bin/bash
	#su - user -c "cd /home/user/E_iquidus && /usr/bin/npm run reindex-rich" > /dev/null 2>&1
	cd /home/user/E_iquidus && /usr/bin/npm run reindex-rich
exit 0



update Peers sudo and regular version:

#!/bin/bash
	#su - user -c "cd /home/user/E_iquidus && /usr/bin/npm run sync-peers" > /dev/null 2>&1
	cd /home/user/E_iquidus && /usr/bin/npm run sync-peers
exit 0



update Transactions sudo and regular version:

#!/bin/bash
	#su - user -c "cd /home/pp/E_iquidus && /usr/bin/node --stack-size=2048 scripts/sync.js index update" > /dev/null 2>&1
	cd /home/pp/E_iquidus && /usr/bin/node --stack-size=2048 scripts/sync.js index update
exit 0

