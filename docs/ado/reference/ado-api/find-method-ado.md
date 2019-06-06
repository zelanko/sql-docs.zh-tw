---
title: Find 方法 (ADO) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: a3f544ae5a38b50ed13ddbafb725c07e0c8a4c8e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697952"
---
# <a name="find-method-ado"></a>Find 方法 (ADO)
搜尋[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)針對符合指定之準則的資料列。 （選擇性） 您可以指定搜尋開始的資料列及從起始的資料列位移的方向。 如果符合準則時，目前的資料列位置會設定上所找到的記錄;否則，位置會設定為結尾 （或起始） 的**資料錄集**。  
  
## <a name="syntax"></a>語法  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>參數  
 *準則*  
 A**字串**包含在搜尋中指定要使用的資料行名稱、 比較運算子和值的陳述式的值。  
  
 *SkipRows*  
 選擇性 *。* A**長**值，其預設值為零，指出目前資料列的資料列位移或*開始*書籤，以便開始搜尋。 根據預設，搜尋會開始對目前資料列。  
  
 *SearchDirection*  
 選擇性 *。* A [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)值，指定是否應該在目前的資料列或下一個可用的資料列的方向搜尋開始搜尋。 不成功的搜尋便會停止在結尾**Recordset**的值是否**adSearchForward**。 不成功的搜尋便會停止在開頭**Recordset**的值是否**adSearchBackward**。  
  
 *啟動*  
 選擇性。 A **Variant**做為搜尋的起始位置的書籤。  
  
## <a name="remarks"></a>備註  
 只能在單一資料行名稱可以指定以*準則*。 這個方法不支援多重資料行搜尋。  
  
 中的比較運算子*準則*可能是" **>** 」 （大於）、 「 **\<** "（小於）、"="（等於）、"> ="（大於或等於）"< ="（小於或等於）、 「 <>"（不等於） 或"like"（模式比對）。  
  
 中的值*準則*可能是字串、 浮點數或日期。 字串值是以單引號或"#"（數字符號） 標記分隔 (比方說，」 狀態 = 'WA' 」 或 「 狀態 = #WA #")。 日期值會以"#"（數字符號） 標記 (例如，"start_date > #7/22/97 #")。 這些值可以包含小時、 分鐘和秒，表示時間戳記，但不是應包含毫秒，或將會發生錯誤。  
  
 比較運算子是"like"，如果字串值可能包含星號 （*） 來尋找一或多個出現的任何字元或子字串。 例如，"等的狀態是\*' 」 符合 Maine 和麻省。 您也可以使用前置和尾端的星號，若要尋找的值範圍內所包含的子字串。 比方說，」 狀態，例如 '\*做為\*' 」 比對 Alaska、 阿肯色州和麻省。  
  
 星號可只在準則字串結尾或開頭和結尾準則字串，如上所示。 您不能使用星號做為前置字元的萬用字元 ('* str')，或內嵌的萬用字元 ('s\*r')。 這會導致錯誤。  
  
> [!NOTE]
>  如果目前的資料列位置未設定之前呼叫，會發生錯誤**尋找**。 這類設定資料列位置的任何方法[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)，然後再呼叫應該呼叫**尋找**。  
  
> [!NOTE]
>  如果您呼叫**尋找**方法上的資料錄集和資料錄集的目前位置位於最後一筆記錄或檔案結尾 (EOF)，您將無法找到任何項目。 您必須呼叫**MoveFirst**方法，將目前的位置/資料指標設定至資料錄集的開頭。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Find 方法範例 (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Index 屬性](../../../ado/reference/ado-api/index-property.md)   
 [Optimize 動態屬性 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
