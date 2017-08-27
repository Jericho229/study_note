#Paypal Note
---

Reference: [Paypal Developer](https://developer.paypal.com/docs/classic/products/express-checkout/)

Created_At:  2017.01.19

---

### 1. Register flow

1. Register Paypal account
* Setting Develop Sandbox Env #1
	* Accepting **Credit Cards** in test transactions.
		* Upgrate account type to **Pro**.  
	* Accepting **Easy Payments** with PayPal Credit in test transactions
		* On the Settings **PayPal Credit** => **On**

* Get API Test Credentials
	* v.zero SDK (TWD not supported)
	* Restful API (***recommend***)
	* NVP/SOAP

---

### 2. Build Express Checkout flow

1. Add the script to your client ```<script src="https://www.paypalobjects.com/api/checkout.js"></script>```

2. Add & Render Check Btn : [Reference](https://developer.paypal.com/docs/integration/direct/express-checkout/integration-jsv4/add-paypal-button/)
	* Options: 
		* Add Debugging tips
		* Setting checkout.js script options
		* Customize Checkout button

3. Choose an integration method
	* Basic #2
		* [API](https://developer.paypal.com/docs/integration/direct/express-checkout/integration-jsv4/basic-integration/) 
		* [Common object definitions](https://developer.paypal.com/docs/api/payments/#definitions)
	* Advanced
		* Reference: [Url](https://developer.paypal.com/docs/integration/direct/express-checkout/integration-jsv4/advanced-integration/) 

### Sandbox #1

* Doc: [Sandbox Overview](https://developer.paypal.com/docs/classic/lifecycle/sb_overview/)

* API: [URL](https://www.sandbox.paypal.com/cgi-bin/webscr)

### Basic Client Sample Code #2

```
<div id="paypal-button"></div> 

<script src="https://www.paypalobjects.com/api/checkout.js"></script>
	
<script>
    paypal.Button.render({
    
        env: 'sandbox', // Optional:  'sandbox' or 'production'
    
        client: {
            sandbox:    'xxxxxxxxx',
            production: 'xxxxxxxxx'
        },
	
        payment: function() {
        
            var env    = this.props.env;
            var client = this.props.client;
        
            return paypal.rest.payment.create(env, client, {
                transactions: [
                    {
                        amount: { total: '1.00', currency: 'USD' }
                    }
                ]
            });
        },
	
        commit: true, // Optional: show a 'Pay Now' button in the checkout flow
	
        onAuthorize: function(data, actions) {
        
            // Optional: display a confirmation page here
        
            return actions.payment.execute().then(function() {
                // Show a success page to the buyer
            });
        }
	
    }, '#paypal-button');
</script>
```

-

1. 頁面表單 
* 送ＡＰI #1
	* Hosted Pay Page(HPP)頁面收到參數，會進行基本檢核
		1. 必要參數
		* 參數長度
		* 交易金額必須大於0 
* 連到HPP(Hosted Pay Page)

* User信用卡驗證
	*	持卡人輸入完成，按下確定按鈕後，即執行如下檢核
		1. 	特店代號是否為該收單行認可的特店
		* 端末機代號是否為該收單行認可的特店所屬的端末機
		* 收單行是否開放權限
		* 線上HPP授權
		* 線上EC授權
		* 支援卡別
		* 卡號檢查碼驗證
		* 卡片有效年月 
* 回傳授權結果 #2

### 2. API #1

* URL: http://xxxx:***9080***/FubonHPP/HPPCheckCtl
	* 防火牆設定須開放連接到 ePayment HPP的通訊埠，目前為 IP:, TCP Port 9080

| Key  | Len| Desc |
|:-- |:--:| --:|
| MERCHANTID | 10~16 | 特店指定單號 |
| TERMINALID | 10~16 | 特店指定單號 |
| ORDERID | <25 | 特店指定單號 |
| TRANSMODE | - | 交易模式<br>0:一般交易<br>1:分期付款交易<br>2:紅利折抵交易
|INSTALL| - | 分期期數, 若為分期付款交易(TRANSMODE=1)，則此參數為必要值，而且必須大於 1
|TRANSAMT|-|交易金額|
|NOTIFYURL|-|特店指定url，由特店自行開發程式接收授權結果做後續處理|
|NOTIFYPARAM|-|特店指定url後面如有需要傳特定參數，參數格式請以”,”連接Ex.userid=AAA,username=BBB|

### 3. 回傳參數說明 #2 -- 待補

| 序號 | 參數 | 參數說明 | 格式 | (最大長度) |
|:-- |:--:| --:| --:| --:|
|1. | MERCHANTID | 特店代號| Numeric| (15)
|2. | TERMINALID | 端末機代號| Numeric | (8)
|3. | ORDERID | 特店指定單號(1~25) | Char | (25)
|4. | TRANSMODE | 交易模式<br>0-一般<br>1-分期<br>2-紅利 | Numeric | (1)
|5. | TRANSAMT | 交易金額| Numeric | (10.2) |
|6. | INSTALL | 分期期數| Numeric | (3) |
|7. | NOTIFYURL | 授權回覆URL| Char | (128) |
|8. | TRANSDATE | 授權日期<br>(YYYYMMDD)| Numeric| (8) |
|9. | TRANSTIME | 授權時間<br>(HHMMSS)| Numeric | (6) |
|10. | RESPONSECODE | 回應碼| Numeric | (3) |
|11. | RESPONSEMSG | 回應訊息| Char | (16) |
|12. | APPROVECODE | 授權碼| Char | (8) |
|13. | SYSORDERID | 系統指定單號| Char | (40) |
|14. | CURRENCYCODE | 交易幣別<br>901-新台幣 | Char | (3)
|15. | TRANSCODE | 交易代碼<br>00-購貨交易<br>01-退貨交易<br>10-購貨取消交易<br>11-退貨取消交易 |Char | (2)
|16. | BATCHNO | 批次號碼| Numeric | (6) |
|17. | FIRSTAMT | 首期金額| Numeric | (10.2) |
|18. | EACHAMT | 每期金額| Numeric | (10.2) |
|19. | FEE | 費用| Numeric | (10.2) |
|20. | INSTALLTYPE | 分期註記<br>I-內含<br>E-外加 | Char | (1)
|21. | REDEMTYPE | 紅利折抵註記<br>1 – 全額折抵<br>2 – 部份折抵|Char | (1) |
|22. | REDEM_USED | 紅利折抵點數| Numeric | (8) |
|23. | REDEM_BALANCE | 紅利餘額| Numeric | (8) |
|24. | CREDITAMT | 卡人自付額| Numeric | (8) |

-
