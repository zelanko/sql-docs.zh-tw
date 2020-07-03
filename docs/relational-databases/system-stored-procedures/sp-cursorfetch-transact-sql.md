---
title: sp_cursorfetch （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f3729587261ab090548ad93f5a1000f621239557
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85868954"
---
# <a name="sp_cursorfetch-transact-sql"></a>sp_cursorfetch (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從資料庫提取一個或多個資料列的緩衝區。 此緩衝區中的資料列群組稱為資料指標的*提取緩衝區*。 sp_cursorfetch 的叫用方式是在表格式資料流 (TDS) 封包中指定 ID = 7。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>引數  
 *cursor*  
 這是由所產生並由 sp_cursoropen 傳回的*控制碼*值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *cursor*是針對**int**輸入值呼叫的必要參數。 如需詳細資訊，請參閱本主題稍後的＜備註＞一節。  
  
 *fetchtype*  
 指定要提取的資料指標緩衝區。 *fetchtype*是選擇性參數，它需要下列其中一個整數輸入值。  
  
|值|名稱|說明|  
|-----------|----------|-----------------|  
|0x0001|FIRST|提取*nrows*資料列的第一個緩衝區。 如果*nrows*等於0，資料指標就會放在結果集之前，而且不會傳回任何資料列。|  
|0x0002|NEXT|提取*nrows*資料列的下一個緩衝區。|  
|0x0004|PREV|提取*nrows*資料列先前的緩衝區。<br /><br /> 注意： FORWARD_ONLY 的資料指標上使用 [上一個] 會傳回錯誤訊息，因為 FORWARD_ONLY 僅支援一個方向的滾動。|  
|0x0008|LAST|提取*nrows*資料列的最後一個緩衝區。 如果*nrows*等於0，資料指標就會放在結果集之後，而且不會傳回任何資料列。<br /><br /> 注意： FORWARD_ONLY 的資料指標上使用 LAST 會傳回錯誤訊息，因為 FORWARD_ONLY 僅支援以一個方向滾動。|  
|0x10|ABSOLUTE|從*rownum*資料列開始，提取*nrows*資料列的緩衝區。<br /><br /> 注意：對動態資料指標或 FORWARD_ONLY 資料指標使用絕對會傳回錯誤訊息，因為 FORWARD_ONLY 僅支援以一個方向滾動。|  
|0x20|RELATIVE|從指定為目前區塊中第一個資料列之資料列的*rownum*值的資料列開始，提取*nrows*資料列的緩衝區。 在此情況下， *rownum*可以是負數。<br /><br /> 注意：對 FORWARD_ONLY 資料指標使用相對，會傳回錯誤訊息，因為 FORWARD_ONLY 僅支援以一個方向滾動。|  
|0x80|REFRESH|從基礎資料表中重新填滿緩衝區。|  
|0x100|INFO|擷取有關資料指標的資訊。 這項資訊會使用*rownum*和*nrows*參數來傳回。 因此，當指定 INFO 時， *rownum*和*nrows*就會成為輸出參數。|  
|0x200|PREV_NOADJUST|它的用途與 PREV 類似。 但是，如果過早遇到結果集的開頭，結果可能會有所不同。|  
|0x400|SKIP_UPDT_CNCY|必須搭配其中一個其他*fetchtype*值使用，但 INFO 除外。|  
  
> [!NOTE]  
>  0x40 值沒有支援。  
  
 如需詳細資訊，請參閱本主題稍後的＜備註＞一節。  
  
 *rownum*  
 這是選擇性參數，用來指定絕對和 INFO *fetchtype*值的資料列位置，方法是只使用輸入或輸出的整數值，或兩者。 *rownum*可作為相對於*fetchtype*位值的資料列位移。 所有其他值都會忽略*rownum* 。 如需詳細資訊，請參閱本主題稍後的＜備註＞一節。  
  
 *nrows*  
 這是選擇性參數，用來指定要提取的資料列數目。 如果未指定*nrows* ，預設值為20個數據列。 若要設定位置而不傳回資料，請指定值0。 當*nrows*套用至*fetchtype* INFO 查詢時，它會傳回該查詢中的資料列總數。  
  
> [!NOTE]  
>  REFRESH *fetchtype*位值會忽略*nrows* 。  
>   
>  如需詳細資訊，請參閱本主題稍後的＜備註＞一節。  
  
## <a name="return-code-values"></a>傳回碼值  
 當您指定位元值 INFO 時，可能傳回的值顯示於以下表格。  
  
> [!NOTE]  
>  如果未傳回任何資料列，緩衝區內容會維持原狀。  
  
|*\<rownum>*|設定為|  
|------------------|------------|  
|如果未開啟|0|  
|如果位於結果集的前面|0|  
|如果位於結果集的後面|-1|  
|如果是 KEYSET 和 STATIC 資料指標|結果集中目前位置的絕對資料列號碼|  
|如果是 DYNAMIC 資料指標|1|  
|如果是 ABSOLUTE|-1 會傳回結果集中的最後一個資料列。<br /><br /> -2 會傳回結果集中的最後第二個資料列，依此類推。<br /><br /> 注意：如果在此情況下要求提取多個資料列，則會傳回結果集的最後兩個數據列。|  
  
|*\<nrows>*|設定為|  
|-----------------|------------|  
|如果未開啟|0|  
|如果是 KEYSET 和 STATIC 資料指標|通常是目前的索引鍵集大小。<br /><br /> **-m** ，如果資料指標是以非同步方式建立，並找到指向這個點的*m*個數據列。|  
|如果是 DYNAMIC 資料指標|-1|  
  
## <a name="remarks"></a>備註  
  
## <a name="cursor-parameter"></a>cursor 參數  
 在有任何提取作業之前，資料指標的預設位置會在結果集的第一個資料列之前。  
  
## <a name="fetchtype-parameter"></a>fetchtype 參數  
 除了 SKIP_UPD_CNCY 以外， *fetchtype*值是互斥的。  
  
 當指定 SKIP_UPDT_CNCY 時，提取或重新整理資料列時，時間戳記資料行值不會寫到索引鍵集資料表。 如果正在更新索引鍵集資料列，時間戳記資料行的值會保留之前的值。 如果正在插入索引鍵集資料列，則不會定義時間戳記資料行的值。  
  
 如果是 KEYSET 資料指標，這表示索引鍵集資料表具有上一次非略過 FETCH 期間所設定的值 (如果已經執行的話)。 如果沒有的話，它的值會是擴展期間所設定。  
  
 如果是 DYNAMIC 資料指標，這表示如果執行略過及重新整理，它會產生與 KEYSET 相同的結果。 如果是其他任何提取類型，索引鍵集資料表會遭到截斷。 這表示正在插入資料列，但是不會定義時間戳記資料行的值。  因此，當您針對 DYNAMIC 資料指標執行 sp_cursorfetch 時，請避免針對 REFRESH 以外的任何作業使用 SKIP_UPDT_CNCY。  
  
 如果提取作業失敗，因為要求的資料指標位置超出結果集，資料指標位置會剛好設定在最後一個資料列的後面。 如果提取作業失敗，因為要求的資料指標位置在結果集前面，資料指標位置會設定在第一個資料列的前面。  
  
## <a name="rownum-parameter"></a>rownum 參數  
 當您使用*rownum*時，會從指定的資料列開始填入緩衝區。  
  
 「絕對」（ *fetchtype* ）值是指*rownum*在整個結果集內的位置。 ABSOLUTE 的負數指定，該作業會從結果集的結尾計算資料列的數目。  
  
 相對於目前緩衝區開頭的資料指標位置， *fetchtype*相對值是指*rownum*的位置。 RELATIVE 的負數指定，資料指標會從目前的資料指標位置逆向進行。  
  
## <a name="nrows-parameter"></a>nrows 參數  
 *Fetchtype*值 REFRESH 和 INFO 會忽略此參數。  
  
 當您指定第一個*nrow*值為0的*fetchtype*值時，資料指標會位於提取緩衝區中沒有資料列的結果集之前。  
  
 當您指定 LAST 的*fetchtype*值，其*nrow*值為0時，資料指標會位於目前提取緩衝區中沒有資料列的結果集之後。  
  
 對於 NEXT、上月、絕對值、相對值和 PREV_NOADJUST 的*fetchtype*值而言， *nrow*值0是不正確。  
  
## <a name="rpc-considerations"></a>RPC 考量  
 RPC 傳回狀態指出索引鍵集大小參數是否為最終的參數，也就是說，索引鍵集或暫存資料表是否正在以非同步方式擴展。  
  
 RPC 狀態參數會設定為下表所示的其中一個值。  
  
|值|說明|  
|-----------|-----------------|  
|0|已成功執行程序。|  
|0x0001|程序失敗。|  
|0x0002|當提取在邏輯上原本應該在結果的前面時，以負數方向提取會造成資料指標位置設定為結果集的開頭。|  
|0x10|自動關閉向前快轉的資料指標。|  
  
 資料列當做一般結果集傳回，也就是資料行格式 (0x2a)、資料列 (0xd1)，後面接著完成 (0xfd)。 中繼資料 Token 的傳送格式與針對 sp_cursoropen 指定的格式相同，也就是：適用於 SQL Server 7.0 使用者的 0x81、0xa5 和 0xa4，依此類推。 資料列狀態指標會當做隱藏資料行傳送，類似於 BROWSE 模式，也就是在每一個資料列結尾，包含資料行名稱 rowstat 和資料類型 INT4。 這個 rowstat 資料行具有下表所列的其中一個值。  
  
|值|說明|  
|-----------|-----------------|  
|0x0001|FETCH_SUCCEEDED|  
|0x0002|FETCH_MISSING|  
  
 因為 TDS 通訊協定如果沒有傳送之前的資料行，就無法傳送尾端狀態資料行，所以會針對遺漏的資料列傳送虛擬資料 (可為 Null 的欄位會設定為 Null，固定長度欄位會適當地設定為 0、空白或是該資料行的預設值)。  
  
 DONE 資料列計數一定是零。 DONE 訊息包含實際結果集的資料列計數，而錯誤或通知訊息則可能會出現在任何 TDS 訊息之間。  
  
 若要要求在 TDS 資料流中傳回有關資料指標選取清單的中繼資料，請將 RPC RETURN_METADATA 輸入旗標設定為 1。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-prev-to-change-a-cursor-position"></a>A. 使用 PREV 來變更資料指標位置  
 假設資料指標 h2 會產生具有下列內容的結果集，目標位置如下所示：  
  
```  
row 1 contents      
row 2 contents  
row 3 contents  
row 4 contents  <-- current position  
row 5 contents   
row 6 contents  
```  
  
 接下來， *nrows*值為5的前一個 sp_cursorfetch 會以邏輯方式將資料指標放在結果集的第一個資料列前兩個數據列。 在這些情況下，資料指標會調整為以第一個資料列開始，並傳回要求的資料列數。 這通常表示，它會傳回之前在 PRIOR 提取緩衝區內的資料列。  
  
> [!NOTE]  
>  這與 RPC 狀態參數設定為 2 的情況一模一樣。  
  
### <a name="b-using-prev_noadjust-to-return-fewer-rows-than-prev"></a>B. 使用 PREV_NOADJUST 傳回少於 PREV 的資料列數  
 PREV_NOADJUST 絕對不會在其傳回的資料列區塊中，包含目前資料指標位置或是該位置之後的任何資料列。 在上一個傳回目前位置之後的資料列的情況下，PREV_NOADJUST 傳回的資料列數少於*nrows*中要求的數目。 在給定之前範例 A 中目前位置的情況下套用 PREV 時，sp_cursorfetch(h2, 4, 1, 5) 會提取以下資料列：  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 但是，當套用 PREV_NOADJUST 時，sp_cursorfetch(h2, 512, 6, 5) 只會提取以下資料列：  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
