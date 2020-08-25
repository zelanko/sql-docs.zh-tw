---
description: Find 方法 (ADO)
title: " (ADO) 的 Find 方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0312fb8a8f91e8b56cb6c29a3a64b3a36bcec69d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775227"
---
# <a name="find-method-ado"></a>Find 方法 (ADO)
搜尋 [記錄集](./recordset-object-ado.md) ，以尋找符合指定準則的資料列。 您可以選擇性地指定搜尋的方向、開始的資料列，以及起始資料列的位移。 如果符合準則，則會在找到的記錄上設定目前的資料列位置。否則，此位置會設定為 **記錄集**的結尾 (或開始) 。  
  
## <a name="syntax"></a>語法  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>參數  
 *準則*  
 **字串**值，包含指定要在搜尋中使用之資料行名稱、比較運算子和值的語句。  
  
 *SkipRows*  
 選擇性。 **Long**值，其預設值為零，指定從目前資料列*到開始搜尋*的資料列位移。 根據預設，搜尋會從目前的資料列開始。  
  
 *SearchDirection*  
 選擇性。 [SearchDirectionEnum](./searchdirectionenum.md)值，指定搜尋是否應該以搜尋方向的目前資料列或下一個可用的資料列為開頭。 如果值是**adSearchForward**，則不成功的搜尋會在**記錄集**的結尾處停止。 如果值是**adSearchBackward**，則不成功的搜尋會在**記錄集**的開頭停止。  
  
 *啟動*  
 選擇性。 作為搜尋開始位置的 **Variant** 書簽。  
  
## <a name="remarks"></a>備註  
 *準則*中只能指定單一資料行的名稱。 這個方法不支援多重資料行搜尋。  
  
 *準則*中的比較運算子可能是 " **>** " (大於) 、"* * \<**" (less than), "=" (equal), "> =" (大於或等於) 、"<=" (小於或等於) 、"<>" (不等於) 或 "like" (模式比對) 。  
  
 *準則*中的值可能是字串、浮點數或日期。 字串值以單引號分隔，或使用 "#" (數位記號) 標記 (例如，"state = ' WA '" 或 "state = #WA #" ) 。 日期值會以 "#" 分隔 (數位記號) 標記 (例如 "start_date > #7/22/97 #" ) 。 這些值可以包含小時、分鐘和秒來表示時間戳記，但不應包含毫秒或錯誤。  
  
 如果比較運算子「贊」，則字串值可能包含星號 ( * ) ，以找出一個或多個字元或子字串的出現次數。 例如，「州（州）」會 \* 符合 Maine 和麻塞諸塞州。 您也可以使用前置和尾端星號來尋找包含在值內的子字串。 例如，「as」之類的「狀態」會 \* \* 符合阿拉斯加、Arkansas 和麻塞諸塞州。  
  
 星號只能用在準則字串的結尾，或在準則字串的開頭和結尾，如上所示。 您無法使用星號做為前置萬用字元 ( ' * str ' ) ，或做為內嵌萬用字元 ( 的 \* r ' ) 。 這會導致錯誤。  
  
> [!NOTE]
>  如果在呼叫 **Find**之前未設定目前的資料列位置，就會發生錯誤。 設定資料列位置的任何方法（例如 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)）都應該在呼叫 **Find**之前呼叫。  
  
> [!NOTE]
>  如果您在記錄集上呼叫 **Find** 方法，且記錄集內目前的位置是在最後一筆記錄或檔案結尾 (EOF) ，您將找不到任何資訊。 您必須呼叫 **MoveFirst** 方法，將目前的位置/資料指標設定為記錄集的開頭。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 Find 方法範例 ](./find-method-example-vb.md)   
 [Index 屬性](./index-property.md)   
 [優化屬性-動態 (ADO) ](./optimize-property-dynamic-ado.md)   
 [Seek 方法](./seek-method.md)