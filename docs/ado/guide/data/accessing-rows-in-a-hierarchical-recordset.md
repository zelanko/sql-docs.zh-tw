---
title: 存取階層式資料錄集中的資料列 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83b8334b4891d0b12cac59030ebf7fced871c5dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294354"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>存取階層式資料錄集 （範例） 中的資料列
下列範例顯示中的步驟需要存取的資料列階層[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **資料錄集**物件從**作者**並**titleauthor**資料表相關的作者 id。

2.  外部迴圈會顯示每位作者的名字和姓氏、 狀態和識別。

3.  附加**Recordset**每個資料列擷取自[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合並指派給*rstTitleAuthor*。

4.  內部迴圈會從每個資料列的四個欄位顯示在 附加**資料錄集**。

 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)屬性設定為**false**基於圖的詳細資訊，以便您可以看到本章變更明確外部迴圈的每個反覆項目中。 若要讓更有效率的程式碼範例，您可以在步驟 2 中的第一行之前的步驟 3 中移動指派，以便指派不只一次執行。 然後設定[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)屬性設 **，則為 true**，以便*rstTitleAuthor*會隱含地自動變更為對應的章節每當*rst*移至新的資料列。

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
 [資料成形概觀](../../../ado/guide/data/data-shaping-overview.md)[欄位物件](../../../ado/reference/ado-api/field-object.md)[欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md) [正式 Shape 文法](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft 資料成形的 OLE DB 服務（ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [所需資料成形的提供者](../../../ado/guide/data/required-providers-for-data-shaping.md)[圖形 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)[圖形中的命令一般](../../../ado/guide/data/shape-commands-in-general.md) [Shape COMPUTE 子句](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic for Applications 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)
