---
title: 存取階層式資料錄集中的資料列 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f45ec72f864c719091adc04a88e181a41124b76
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270167"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>存取資料列中的階層式資料錄集 （範例）
下列範例說明中的步驟需要存取的資料列階層式[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **資料錄集**物件從**作者**和**titleauthor**資料表相關的作者 id。

2.  外部迴圈會顯示每位作者的名字和姓氏、 狀態和識別。

3.  附加**資料錄集**的每個資料列擷取自[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合並指派給*rstTitleAuthor*。

4.  內部迴圈會從每個資料列的四個欄位顯示在附加**資料錄集**。

 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)屬性設定為**false**基於圖的詳細資訊，以便您可以看到本章變更明確外部迴圈的每個反覆項目中。 若要進行更有效率的程式碼範例，您可以在步驟 2 中的第一行之前的步驟 3 中移動指派，以便不只一次執行作業。 然後設定[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)屬性**true**，如此*rstTitleAuthor*會以隱含方式並自動變更為對應的章節每當*rst*移到新的資料列。

## <a name="example"></a>範例

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>另請參閱
 [資料成形概觀](../../../ado/guide/data/data-shaping-overview.md)[欄位物件](../../../ado/reference/ado-api/field-object.md)[欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md) [正式圖形文法](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft 資料成形 OLE DB 的服務（ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [資料成形所需提供者](../../../ado/guide/data/required-providers-for-data-shaping.md)[圖形 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)[圖形中的命令一般](../../../ado/guide/data/shape-commands-in-general.md)[圖形 COMPUTE 子句](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic 應用程式函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)
