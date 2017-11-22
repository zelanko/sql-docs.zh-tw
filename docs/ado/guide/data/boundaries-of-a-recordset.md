---
title: "資料錄集的界限 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67a300e30522a5f02bb6c33409a062a3c2434643
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="boundaries-of-a-recordset"></a>資料錄集的界限
**資料錄集**支援**BOF**和**EOF**區分的開頭和結尾，分別資料集的屬性。 您可以將**BOF**和**EOF**為位於開頭和結尾的 「 虛設 」 記錄**資料錄集**。 計算**BOF**和**EOF**，我們的範例**資料錄集**現在看起來會像這樣：  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|得以 Bob 有機曬的梨子|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle 酸菜|45.6000|  
|51|馬普乾蘋果|53.0000|  
|74|長壽豆腐|10.0000|  
|EOF|||  
  
 當資料指標移動到超過最後一筆記錄，以後**EOF**設為**True**; 否則它的值是**False**。 同樣地，當資料指標將第一筆記錄之前, **BOF**設為**True**; 否則它的值是**False**。 這些屬性通常用於列舉記錄在資料集中，如下列 JScript 程式碼片段所示。  
  
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
  
 如果兩個**BOF**和**EOF**是**True**、**資料錄集**物件是空的。 這兩個屬性將會**False**新開啟的非空白的**資料錄集**物件。 您可以使用**BOF**和**EOF**屬性一起，以判斷**資料錄集**物件是空的或不是，如下列 JScript 程式碼片段所示。  
  
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
  
 這種配置適用於所有類型的資料指標和獨立於基礎提供者。 如果您嘗試判斷的序列**資料錄集**物件，方法是檢查其**RecordCount**屬性值是否為零 (0)，您必須採取預防措施，以使用適當的資料指標和提供者，支援傳回的結果中的記錄數目。  
  
 如果您刪除中的最後一個剩餘記錄**資料錄集**物件時，游標會處於不定狀態。 **BOF**和**EOF**屬性可能會維持**False**直到您嘗試重新調整位置目前的記錄，根據提供者。 如需詳細資訊，請參閱[使用 Delete 方法刪除記錄](../../../ado/guide/data/deleting-records-using-the-delete-method.md)。
