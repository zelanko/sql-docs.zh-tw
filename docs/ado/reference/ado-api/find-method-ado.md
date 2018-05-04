---
title: Find 方法 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32da5045e7cd588c555c6e9fed7d5d3371fded2b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="find-method-ado"></a>Find 方法 (ADO)
搜尋[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)符合指定之準則的資料列。 （選擇性） 您可以指定搜尋開始的資料列及從起始的資料列位移的方向。 如果符合條件時，所找到的記錄; 上設定目前資料列位置否則，會結束 （或開始） 的設定位置**資料錄集**。  
  
## <a name="syntax"></a>語法  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>參數  
 *準則*  
 A**字串**值，包含在搜尋中指定要使用的資料行名稱、 比較運算子和值的陳述式。  
  
 *SkipRows*  
 選擇性*。* A**長**值，其預設值為零，會指定從目前資料列的資料列位移或*啟動*來開始搜尋的書籤。 根據預設，搜尋會啟動目前的資料列。  
  
 *SearchDirection*  
 選擇性*。* A [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)值，指定是否應該開始搜尋在目前的資料列或下一個可用的資料列中搜尋方向。 失敗的搜尋會停止在結尾**資料錄集**如果值為**adSearchForward**。 失敗的搜尋會停止在開頭**資料錄集**如果值為**adSearchBackward**。  
  
 *啟動*  
 選擇性。 A **Variant**做為搜尋的起始位置的書籤。  
  
## <a name="remarks"></a>備註  
 只能在單一資料行名稱中可能指定*準則*。 這個方法不支援多重資料行搜尋。  
  
 中的比較運算子*準則*可能是"**>**」 （大於）、"**\<**"（小於）、"="（等於）、"> ="（大於或等於）"< ="（小於或等於）、"<>"（不等於） 或 [讚] （模式比對）。  
  
 中的值*準則*可能是字串、 浮點數或日期。 字串值會以單引號或"#"（數字符號） 標記分隔 (例如，"狀態 = 'WA'"或"狀態 = #WA #")。 日期值會以"#"（數字符號） 標記分隔 (例如，"start_date > #7/22/97 #")。 這些值可以包含小時、 分鐘和秒，表示時間戳記，但不是應包含毫秒，或將發生錯誤。  
  
 如果比較運算子是 [讚]，字串值可能會包含星號 （*） 來尋找一個或多個出現的任何字元或子字串。 例如，"類似的狀態是\*'"符合 Maine 和 Massachusetts。 您也可以使用以尋找包含值範圍內的子字串的開頭和尾端的星號。 比方說，「 狀態類似 '\*為\*'"比對阿拉斯加、 阿肯色州和 Massachusetts。  
  
 星號可用只能在準則字串結尾或開頭和結尾準則字串，如上所示。 您無法使用星號做為前置萬用字元 ('* str')，或當做內嵌的萬用字元 ('s\*r')。 這會導致錯誤。  
  
> [!NOTE]
>  如果未設定目前的資料列位置之前呼叫，會發生錯誤**尋找**。 例如，設定資料列位置的任何方法[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)，應該會在呼叫之前呼叫**尋找**。  
  
> [!NOTE]
>  如果您呼叫**尋找**資料錄集和目前資料錄集中的位置上的方法是在最後一筆記錄或檔案結尾 (EOF)，您將找不到任何項目。 您需要呼叫**MoveFirst**方法，以加入資料錄集的開頭設定目前的位置/資料指標。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [尋找方法範例 (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Index 屬性](../../../ado/reference/ado-api/index-property.md)   
 [最佳化屬性動態 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
