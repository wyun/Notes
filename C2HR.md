# Access C2HR Paycheck history

1. set webpage date range first. 

2. run this code in console.
```
var res = [];
```
3.  run this code to generate 'PDF' files.
```
var rows = document.getElementsByClassName('linkRow');
for (var i in rows) {
    var link = rows[i].getAttribute('onclick');
    link = link.replace("document.location='/CheckDistribution.do", "https://c2hr.app.vumc.org/GetCheckDetail.do")
    link = link.replace("';", "")
    link = link.replace("html", "pdf")
    var dateObj = new Date(Date.parse(rows[i].childNodes[1].innerText));
    var dateName = 'VU_Check_' + dateObj.toISOString().split('T')[0];
    var cookie = 'Cookie: CID=BgAAALFtaXia4gH6Z4d8y0ldcLI=; _ga=GA1.2.2110581409.1604348420; _rollupGa=GA1.2.2110581409.1604348420; _imp_di_pc_=AXmKpmAAAAAAYTzuuT0IXLxvkqZRV+Zg; amplitude_id_ea4b39ed3ea19d79b73a7857abb47928vumc.org=eyJkZXZpY2VJZCI6IjVmY2Y1OWM0LTIyZDMtNDljZC04MGU1LTgwN2JmZTgzYjk0OFIiLCJ1c2VySWQiOm51bGwsIm9wdE91dCI6ZmFsc2UsInNlc3Npb25JZCI6MTYzNTM0ODY5MjUzOSwibGFzdEV2ZW50VGltZSI6MTYzNTM0ODY5MjUzOSwiZXZlbnRJZCI6MCwiaWRlbnRpZnlJZCI6MCwic2VxdWVuY2VOdW1iZXIiOjB9; BIGipServer~legacy_services~c2hr=!BNFxDXmuTMXKXopN8QKCAZBWTu+mcJU9bR1EwGLE9f9EbZAA4NM0PxGOBKcMGr4AFcAB4aGzSnmkZZY=; JSESSIONID=f_q8O4EDanpwQO-uehx7SdiI7l5D2eOKl-DhqhHi_PO5I1NqPyDN!1537306348; c2hrIdVerification=-2093850977194468551a-4859255798481896911';
    res.push(`curl -H \$'${cookie}' '${link}' -o ${dateName}.pdf\n`);
}
```
4. ignore errors. then run `res.join('')`
5. Copy the result into `paycheck.sh`. 
6. `chmod 755 paycheck.sh`
7. Run `./paycheck.sh` in command line.

