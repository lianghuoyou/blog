去尾
```javascript
'12344448888888800000000'
.split('').reverse().join('')
.replace(/\d{8}(?=\d)/g, '亿').replace(/\d{4}(?=\d)/g, '万')
.split('').reverse().join('')

// "123万亿亿"
```
保留小数，超过21位变成科学计数法时会不准
```javascript
function f(value) {
    value = value + '';
    var l1 = value.length - 1; // -1 万亿前至少要有一位数
    var l4 = parseInt(l1 / 4); // '0000' * m
    var ly = parseInt(l4 / 2); // '00000000' * n
    var lw = l4 % 2; // '0000' * n
    var v = value / (Math.pow(100000000, ly) * Math.pow(10000, lw));
    return (+v.toFixed(1)) + // 保留n位小数, +:小数0不保留
        Array(lw + 1).join('万') +
        Array(ly + 1).join('亿')
}
```
最优
```javascript
function f(value) {
    for (var i = 0; true; i++) {
        var v = value / 10000;
        if (v < 1) break;
        value = v;
    }
    return (+value.toFixed(1)) + // 保留n位小数, +:小数0不保留
        Array(i % 2 + 1).join('万') +
        Array(parseInt(i / 2) + 1).join('亿')
}
```
