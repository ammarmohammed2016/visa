# visa
var express = require('express');
var app = express();

var jwt = require('jsonwebtoken');
app.get('/get', function (req, res) {
    jwt.sign({
        amount: 1000,//Product Ammout
        serviceType: 'AAA books website',
        msisdn: 9647826520965,
        orderId: 12345,//optional
        redirectUrl: "http://iraqhostweb.com/",//optional
    }, '8c246f1baec3094ad95b361a7610b3992f658b28672deef79a42df1efdb28261', {
        expiresIn: '4h'
    }, function (err, token) {
        request.post({
            url: 'https://test.zaincash.iq/transaction/init',
            form: {
                token: token,
                merchantId: "57bb3b1867b33971899bd48e",
                lang: "ar",//optional
            }
        }, function (err, httpResponse, body) {
            var body = JSON.parse(body); // response of body { id : "asdae123asd123asd" }
            if (body.id)
                return res.redirect('https://test.zaincash.iq/transaction/pay?id=' + body.id);
            return res.redirect('/payment?msg=cannot_generate_token');
        })
    });
});
app.listen(2000);
