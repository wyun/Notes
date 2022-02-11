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
    var group = rows[i].childNodes[3].innerText;
    var dateObj = new Date(Date.parse(rows[i].childNodes[1].innerText));
    var dateName = 'VU_Check_' + group + '_' + dateObj.toISOString().split('T')[0];
    var cookie = 'Cookie: CID=BgAAALFtcLI=; _.....51a3889994878493843098';
    res.push(`curl -H \$'${cookie}' '${link}' -o ${dateName}.pdf`);
}
```
4. ignore errors. then run `console.log(res.join('\n'));`
5. Copy the result into `paycheck.sh`. 
6. `chmod 755 paycheck.sh`
7. Run `./paycheck.sh` in command line.

