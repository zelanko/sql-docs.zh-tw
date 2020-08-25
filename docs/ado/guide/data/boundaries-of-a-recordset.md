---
description: 資料錄集的界限
title: 記錄集的界限 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
author: rothja
ms.author: jroth
ms.openlocfilehash: aec0ad3065deb60f99f672712c085fe054885d27
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806382"
---
# <a name="boundaries-of-a-recordset"></a>資料錄集的界限
**記錄集** 支援 **BOF** 和 **EOF** 屬性，分別描繪出資料集的開頭和結尾。 您可以將 **BOF** 和 **EOF** 視為位於 **記錄集**開頭和結尾的「虛設」記錄。 計算 **BOF** 和 **EOF**，我們的範例 **記錄集** 現在看起來像這樣：  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|轉爐|||  
|7|圖報 Bob 的有機蒙娜 Pears|30.0000|  
|14|豆腐|23.2500|  
|28|Rssle 酸菜|45.6000|  
|51|Manjimup 蒙娜蘋果|53.0000|  
|74|Longlife Tofu|10.0000|  
|EOF|||  
  
 當資料指標移動到最後一筆記錄之後， **EOF** 會設定為 **True**;否則，其值為 **False**。 同樣地，當資料指標在第一筆記錄之前移動時， **BOF** 會設定為 **True**;否則，其值為 **False**。 這些屬性通常用來列舉資料集中的記錄，如下列 JScript 程式碼片段所示。  
  
```  
while (objRecordset.EOF != true)   
{  
   // Work on the current record.  
   ...  
   // Advance the cursor forward to the next record.  
   objRecordset.MoveNext();  
}  
or  
while (objRecordset.BOF != true)   
{  
   // Work on the current record.  
   ...  
   // Move the cursor to the previous record.  
   objRecordset.MovePrevious();  
}  
```  
  
 如果 **BOF** 和 **EOF** 都是 **True**，則 **記錄集** 物件是空的。 新開啟、非空白的**記錄集**物件的兩個屬性都是**False** 。 您可以同時使用 **BOF** 和 **EOF** 屬性來判斷 **記錄集** 物件是否為空白，如下列 JScript 程式碼片段所示。  
  
```  
if (objRecordset.EOF == true && objRecordset.BOF == true)  
{  
   WScript.Echo("we got an empty dataset.");  
}  
else  
{  
   WScript.Echo("we got a full dataset.");  
}  
```  
  
 此配置適用于所有類型的資料指標，且與基礎提供者無關。 如果您嘗試判斷 **記錄集** 物件的 emptiness，方法是檢查其 **RecordCount** 屬性值是否為零 (0) ，您必須採取預防措施，以使用支援在結果中傳回記錄數目的適當資料指標和提供者。  
  
 如果您刪除 **記錄集** 物件中的最後一筆記錄，資料指標會保持在不定的狀態。 在您嘗試重新置放目前的記錄之前（視提供者而定）， **BOF** 和 **EOF** 屬性可能會維持 **False** 。 如需詳細資訊，請參閱 [使用 Delete 方法刪除記錄](./deleting-records-using-the-delete-method.md)。