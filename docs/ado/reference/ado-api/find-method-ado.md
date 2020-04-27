---
title: Find 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f394d5e3b3021ca240675d6979152c63b903190
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918621"
---
# <a name="find-method-ado"></a>Find 方法 (ADO)
搜尋[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，尋找符合指定準則的資料列。 您可以選擇性地指定搜尋的方向、起始資料列，以及起始資料列的位移。 如果符合條件，就會在找到的記錄上設定目前的資料列位置。否則，位置會設定為**記錄集**的結束（或開始）。  
  
## <a name="syntax"></a>語法  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>參數  
 *指標*  
 **字串**值，其中包含指定要在搜尋中使用之資料行名稱、比較運算子和值的語句。  
  
 *SkipRows*  
 選擇性。 **Long**值，其預設值為零，指定從目前資料列或*起始*書簽開始搜尋的資料列位移。 根據預設，搜尋將會從目前的資料列開始。  
  
 *SearchDirection*  
 選擇性。 [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)值，指定搜尋是否應在目前資料列或搜尋方向的下一個可用資料列開始。 如果值為**adSearchForward**，則會在**記錄集**的結尾停止不成功的搜尋。 如果值為**adSearchBackward**，則會在**記錄集**的開頭停止不成功的搜尋。  
  
 *啟動*  
 選擇性。 做為搜尋開始位置的**Variant**書簽。  
  
## <a name="remarks"></a>備註  
 *條件*中只能指定單一資料行名稱。 這個方法不支援多重資料行的搜尋。  
  
 *準則*中的比較運算子可能是 "**>**" （大於）、"**\<**" （小於）、"=" （等於）、">=" （大於或等於）、"<=" （小於或等於）、"<>" （不等於）或 "like" （模式比對）。  
  
 [*準則*] 中的值可以是字串、浮點數或日期。 字串值會以單引號或 "#" （數位記號）標記分隔（例如，"state = ' WA '" 或 "state = #WA #"）。 日期值會以 "#" （數位記號）標記分隔（例如，"start_date > #7/22/97 #"）。 這些值可以包含小時、分鐘和秒來表示時間戳記，但不應包含毫秒或錯誤。  
  
 如果比較運算子是 "like"，則字串值可能包含星號（*），以尋找一或多個出現的任何字元或子字串。 例如，「像是 ' m\*'」的狀態會符合 Maine 和麻塞諸塞州。 您也可以使用開頭和尾端的星號來尋找包含在值內的子字串。 例如，「\*如 ' as\*'」之類的狀態會符合阿拉斯加、Arkansas 和麻塞諸塞州。  
  
 星號只能用在準則字串的結尾，或在準則字串的開頭和結尾，如上所示。 您不能使用星號做為開頭的萬用字元（' * str '），也不能當做內嵌萬用字元\*（的 r '）。 這會造成錯誤。  
  
> [!NOTE]
>  如果未在呼叫**Find**之前設定目前的資料列位置，就會發生錯誤。 設定資料列位置的任何方法（例如[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)），都應該在呼叫**Find**之前呼叫。  
  
> [!NOTE]
>  如果您在記錄集上呼叫**Find**方法，而且記錄集的目前位置是在最後一筆記錄或檔案結尾（EOF），您就找不到任何專案。 您必須呼叫**MoveFirst**方法，將目前的位置/資料指標設定為記錄集的開頭。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Find 方法範例（VB）](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Index 屬性](../../../ado/reference/ado-api/index-property.md)   
 [優化屬性-動態（ADO）](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
