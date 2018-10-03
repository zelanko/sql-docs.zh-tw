---
title: 資料錄集的界限 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c9e05a45b5f035a500e210c991a33216be318ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633446"
---
# <a name="boundaries-of-a-recordset"></a>資料錄集的界限
**資料錄集**支援**BOF**並**EOF**以框出開頭和結尾，分別將資料集的屬性。 您可以想像**BOF**並**EOF**為位於開頭和結尾的 「 虛設 」 記錄**資料錄集**。 計算**BOF**並**EOF**，我們的範例**資料錄集**現在看起來會像這樣：  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|得以 Bob 有機曬的梨子|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle 酸菜|45.6000|  
|51|柳乾蘋果|53.0000|  
|74|長壽豆腐|10.0000|  
|EOF|||  
  
 當游標移至最後一筆記錄，將**EOF**設為 **，則為 True**; 否則它的值是**False**。 同樣地，當游標移第一筆記錄，再**BOF**設為 **，則為 True**; 否則它的值是**False**。 下列 JScript 程式碼片段所示，這些屬性通常會用來列舉，資料集中的記錄。  
  
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
  
 如果兩個**BOF**並**EOF**會 **，則為 True**，則**資料錄集**物件是空的。 這兩個屬性會**假**的新開啟的是，非空白**資料錄集**物件。 您可以使用**BOF**並**EOF**屬性，在一起，以決定如果**資料錄集**物件是空的或不是，如下列 JScript 程式碼片段所示。  
  
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
  
 此配置適用於所有類型的資料指標，而且都無關的基礎提供者。 如果您嘗試判斷的空白**資料錄集**物件，方法是檢查其**RecordCount**屬性值為零 (0) 或不，您必須採取預防措施，以使用適當的資料指標和提供者，支援傳回的結果中的記錄數目。  
  
 如果您刪除中的最後一個剩餘記錄**資料錄集**物件時，游標會處於不定狀態。 **BOF**並**EOF**屬性可能會維持**False**直到您嘗試調整目前記錄的位置，視提供者。 如需詳細資訊，請參閱 <<c0> [ 使用 Delete 方法刪除記錄](../../../ado/guide/data/deleting-records-using-the-delete-method.md)。
