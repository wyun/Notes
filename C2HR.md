# Access C2HR Paycheck history

1. set webpage date range first. 

2. run this code in console.
```
var res = [];
```
3.  Copy cookie from browser, change it to code below. run this code to generate 'PDF' files.
```JS
var rows = document.getElementsByClassName('linkRow');
for (var i in rows) {
    var link = rows[i].getAttribute('onclick');
    link = link.replace("document.location='/CheckDistribution.do", "https://c2hr.app.vumc.org/GetCheckDetail.do")
    link = link.replace("';", "")
    link = link.replace("html", "pdf")
    var dateObj = new Date(Date.parse(rows[i].childNodes[1].innerText));
    var dateName = 'VU_Check_' + dateObj.toISOString().split('T')[0];
    var cookie = 'Cookie: CID=...............................................8551a-4859255798481896911';
    res.push(`curl -H \$'${cookie}' '${link}' -o ${dateName}.pdf\n`);
}
```
4. ignore errors. then run `res.join('')`
5. Copy the result into `paycheck.sh`. 
6. `chmod 755 paycheck.sh`
7. Run `./paycheck.sh` in command line.

