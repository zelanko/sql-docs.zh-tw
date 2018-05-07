---
title: sp_cursorfetch (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9bbffe757b6b9c76bc1eb0b95e883f3d4d30b461
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spcursorfetch-transact-sql"></a>sp_cursorfetch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從資料庫提取一個或多個資料列的緩衝區。 這個緩衝區中的資料列群組稱為資料指標的*提取緩衝區*。 sp_cursorfetch 的叫用方式是在表格式資料流 (TDS) 封包中指定 ID = 7。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>引數  
 *cursor*  
 是*處理*所產生值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 sp_cursoropen 傳回。 *資料指標*是必要的參數呼叫**int**輸入值。 如需詳細資訊，請參閱本主題稍後的＜備註＞一節。  
  
 *fetchtype*  
 指定要提取的資料指標緩衝區。 *fetchtype*是需要下列其中一個下列整數輸入值的選擇性參數。  
  
|Value|名稱|Description|  
|-----------|----------|-----------------|  
|0x0001|FIRST|擷取的第一個緩衝區*nrows*資料列。 如果*nrows*等於 0，資料指標位於結果集之前，會傳回任何資料列。|  
|0x0002|NEXT|擷取下一個緩衝區*nrows*資料列。|  
|0x0004|PREV|擷取上一個緩衝區*nrows*資料列。<br /><br /> 注意： 將 PREV 用於 FORWARD_ONLY 資料指標傳回錯誤訊息，因為 FORWARD_ONLY 只支援一個方向的捲動。|  
|0x0008|LAST|擷取的最後一個緩衝區*nrows*資料列。 如果*nrows*等於 0，將游標放在結果集，並會傳回任何資料列之後。<br /><br /> 注意： 將 LAST 用於 FORWARD_ONLY 資料指標傳回錯誤訊息，因為 FORWARD_ONLY 只支援一個方向的捲動。|  
|0x10|ABSOLUTE|擷取的緩衝區*nrows*資料列開始*rownum*資料列。<br /><br /> 注意： 將 ABSOLUTE 用於 DYNAMIC 資料指標或 FORWARD_ONLY 資料指標傳回錯誤訊息，因為 FORWARD_ONLY 只支援一個方向的捲動。|  
|0x20|RELATIVE|擷取緩衝區的*nrows*為指定的資料列開始的資料列*rownum*目前區塊中的第一個資料列中的資料列的值。 在此情況下*rownum*可以是負數。<br /><br /> 注意： 將 RELATIVE 用於 FORWARD_ONLY 資料指標傳回錯誤訊息，因為 FORWARD_ONLY 只支援一個方向的捲動。|  
|0x80|REFRESH|從基礎資料表中重新填滿緩衝區。|  
|0x100|INFO|擷取有關資料指標的資訊。 這項資訊由使用*rownum*和*nrows*參數。 因此，當指定 INFO 時， *rownum*和*nrows*會成為輸出參數。|  
|0x200|PREV_NOADJUST|它的用途與 PREV 類似。 但是，如果過早遇到結果集的開頭，結果可能會有所不同。|  
|0x400|SKIP_UPDT_CNCY|必須與其中一個其他使用*fetchtype*除了資訊的值。|  
  
> [!NOTE]  
>  0x40 值沒有支援。  
  
 如需詳細資訊，請參閱本主題稍後的＜備註＞一節。  
  
 *rownum*  
 這是選擇性參數，用來指定 ABSOLUTE 和資訊的資料列位置*fetchtype*透過只將整數值的輸入、 輸出，或兩者的值。 *rownum*做為資料列位移*fetchtype*位元值 RELATIVE。 *rownum*會忽略所有其他值。 如需詳細資訊，請參閱本主題稍後的＜備註＞一節。  
  
 *nrows*  
 這是選擇性參數，用來指定要提取的資料列數目。 如果*nrows*未指定，預設值是 20 個資料列。 若要設定的位置，而不傳回資料，指定值為 0。 當*nrows*套用至*fetchtype* INFO 查詢時，它會傳回資料列總數中該查詢。  
  
> [!NOTE]  
>  *nrows*會忽略重新整理*fetchtype*位元值。  
>   
>  如需詳細資訊，請參閱本主題稍後的＜備註＞一節。  
  
## <a name="return-code-values"></a>傳回碼值  
 當您指定位元值 INFO 時，可能傳回的值顯示於以下表格。  
  
> [!NOTE]  
>  ： 如果不傳回任何資料列，緩衝區內容會維持原狀。  
  
|*\<rownum >*|設定為|  
|------------------|------------|  
|如果未開啟|0|  
|如果位於結果集的前面|0|  
|如果位於結果集的後面|-1|  
|如果是 KEYSET 和 STATIC 資料指標|結果集中目前位置的絕對資料列號碼|  
|如果是 DYNAMIC 資料指標|1|  
|如果是 ABSOLUTE|-1 會傳回結果集中的最後一個資料列。<br /><br /> -2 會傳回結果集中的最後第二個資料列，依此類推。<br /><br /> 附註： 如果要在此情況下提取要求多個資料列，則會傳回結果集的最後兩個資料列。|  
  
|*\<nrows >*|設定為|  
|-----------------|------------|  
|如果未開啟|0|  
|如果是 KEYSET 和 STATIC 資料指標|通常是目前的索引鍵集大小。<br /><br /> **– m**非同步建立與資料指標是否*m*到這個點找到的資料列。|  
|如果是 DYNAMIC 資料指標|-1|  
  
## <a name="remarks"></a>備註  
  
## <a name="cursor-parameter"></a>cursor 參數  
 在有任何提取作業之前，資料指標的預設位置會在結果集的第一個資料列之前。  
  
## <a name="fetchtype-parameter"></a>fetchtype 參數  
 除了 skip_upd_cncy 以外， *fetchtype*值都會互斥。  
  
 當指定 SKIP_UPDT_CNCY 時，提取或重新整理資料列時，時間戳記資料行值不會寫到索引鍵集資料表。 如果正在更新索引鍵集資料列，時間戳記資料行的值會保留之前的值。 如果正在插入索引鍵集資料列，則不會定義時間戳記資料行的值。  
  
 如果是 KEYSET 資料指標，這表示索引鍵集資料表具有上一次非略過 FETCH 期間所設定的值 (如果已經執行的話)。 如果沒有的話，它的值會是擴展期間所設定。  
  
 如果是 DYNAMIC 資料指標，這表示如果執行略過及重新整理，它會產生與 KEYSET 相同的結果。 如果是其他任何提取類型，索引鍵集資料表會遭到截斷。 這表示正在插入資料列，但是不會定義時間戳記資料行的值。  因此，當您針對 DYNAMIC 資料指標執行 sp_cursorfetch 時，請避免針對 REFRESH 以外的任何作業使用 SKIP_UPDT_CNCY。  
  
 如果提取作業失敗，因為要求的資料指標位置超出結果集，資料指標位置會剛好設定在最後一個資料列的後面。 如果提取作業失敗，因為要求的資料指標位置在結果集前面，資料指標位置會設定在第一個資料列的前面。  
  
## <a name="rownum-parameter"></a>rownum 參數  
 當您使用*rownum*，緩衝區已滿的指定資料列開始。  
  
 *Fetchtype*值 ABSOLUTE 會參考位置的*rownum*內整個結果集。 ABSOLUTE 的負數指定，該作業會從結果集的結尾計算資料列的數目。  
  
 *Fetchtype*值 RELATIVE 會參考位置的*rownum*相對於目前緩衝區開頭的資料指標的位置。 RELATIVE 的負數指定，資料指標會從目前的資料指標位置逆向進行。  
  
## <a name="nrows-parameter"></a>nrows 參數  
 *Fetchtype*值 REFRESH 和 INFO 會忽略這個參數。  
  
 當您指定*fetchtype*具有第一個值*nrow*值為 0，將游標定位於結果集提取緩衝區內沒有任何資料列的前面。  
  
 當您指定*fetchtype*具有的最後一個值*nrow*值為 0，資料指標會位於結果集目前的提取緩衝區內沒有任何資料列之後。  
  
 如*fetchtype*值的下一步、 PREV、 ABSOLUTE、 RELATIVE 和 PREV_NOADJUST， *nrow*無效的值為 0。  
  
## <a name="rpc-considerations"></a>RPC 考量  
 RPC 傳回狀態指出索引鍵集大小參數是否為最終的參數，也就是說，索引鍵集或暫存資料表是否正在以非同步方式擴展。  
  
 RPC 狀態參數會設定為下表所示的其中一個值。  
  
|Value|설명|  
|-----------|-----------------|  
|0|已成功執行程序。|  
|0x0001|程序失敗。|  
|0x0002|當提取在邏輯上原本應該在結果的前面時，以負數方向提取會造成資料指標位置設定為結果集的開頭。|  
|0x10|自動關閉向前快轉的資料指標。|  
  
 資料列當做一般結果集傳回，也就是資料行格式 (0x2a)、資料列 (0xd1)，後面接著完成 (0xfd)。 中繼資料 Token 的傳送格式與針對 sp_cursoropen 指定的格式相同，也就是：適用於 SQL Server 7.0 使用者的 0x81、0xa5 和 0xa4，依此類推。 資料列狀態指標會當做隱藏資料行傳送，類似於 BROWSE 模式，也就是在每一個資料列結尾，包含資料行名稱 rowstat 和資料類型 INT4。 這個 rowstat 資料行具有下表所列的其中一個值。  
  
|Value|Description|  
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
  
 接下來，sp_cursorfetch PREV 具有*nrows* 5 的值會以邏輯方式將結果集的第一個資料列之前的資料指標兩個資料列。 在這些情況下，資料指標會調整為以第一個資料列開始，並傳回要求的資料列數。 這通常表示，它會傳回之前在 PRIOR 提取緩衝區內的資料列。  
  
> [!NOTE]  
>  這與 RPC 狀態參數設定為 2 的情況一模一樣。  
  
### <a name="b-using-prevnoadjust-to-return-fewer-rows-than-prev"></a>B. 使用 PREV_NOADJUST 傳回少於 PREV 的資料列數  
 PREV_NOADJUST 絕對不會在其傳回的資料列區塊中，包含目前資料指標位置或是該位置之後的任何資料列。 在 PREV 傳回資料列目前的位置之後的情況下，PREV_NOADJUST 會傳回較少的資料列中要求*nrows*。 指定的目前位置在範例中的更早版本，當套用 PREV 時，sp_cursorfetch (h2，4，1，5) 會提取以下資料列：  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 不過，當套用 PREV_NOADJUST 時，sp_cursorfetch (h2，512，6，5) 會提取以下資料列：  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_cursoropen &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
