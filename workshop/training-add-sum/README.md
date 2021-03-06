Golang 程式設計題目(簡單加總分工)
===

###### tags: `訓練`


## 說明：
:::info

shal1 是一種不可逆加密方式。

加密是指固定的input丟入hash處理之後，output的結果也一定是固定。

以下計算方式是這樣:

1. 將某個數字，從數字轉換成字串，丟入shal1做hash。
2. 每個hash結果會有20個byte，將每個byte強制轉成數字。
例如把"0"丟進去，拿到的output是這樣：
[182 88 159 198 171 13 200 44 241 32 153 209 194 212 10 185 148 232 65 12]
4. 將這20個byte轉換出來的數字做加總。
5. 從0~99999999的數字(1億個數字)都經過以上步驟後，全部做加總得出結果。

:::

## 題目：
:::info
1. 請先將以下範例在自己電腦跑過一次，並記錄花費時間。
2. 請用goroutine改寫，目標是加總數字正確，花費時間少1/3以上，如範例花費了23秒，則希望可以在16秒內處理完成。
3. 如果能夠將花費時間減少至1/2秒內，請來找我，請你喝飲料(目前自己隨意試試，不好辦到)。
4. 以上是以公司配發的mac(2017 pro)為標準，如果使用其他設備，時間不好斟酌可以找我討論。
5. 禁止作弊，例如用範例去跑的時候，故意讓電腦是正處於很忙碌的狀態。

:::


``` go
package main

import (
	"crypto/sha1"
	"log"
	"strconv"
	"time"
)

func v1() {


	var (
		sum    int
		target = 100000000
	)

	t1 := time.Now()
	for i := 0; i < target; i++ {

		num := strconv.Itoa(i)

		shalResult := sha1.Sum([]byte(num))

		for j := 0; j < 20; j++ {
			sum += int(shalResult[j])
		}
	}
	t2 := time.Since(t1)
	log.Println("加總數字:", sum, "花費時間", t2)
    	// 2020/06/02 16:54:44 加總數字: 255001985043 花費時間 23.777596654s
}

```
