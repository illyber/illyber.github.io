---
title: chown和chgrp
categories:
  - Linux
date: 2024-04-02 05:20
tags:
  - 所有权
---

---
# chown
```shell
#改变所有者和所属组
chown [-R] hdg a.txt		#改变所有者为hdg
chgrp [-R] hdg a.txt		#改变所属组为hdg
chown [-R] hdg:root a.txt	#将a.txt的所有者改为hdg, 所属组改为root
#也可将colon改为dot
chown [-R] hdg.root a.txt
```

# chgrp




---
