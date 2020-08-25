---
description: '存取階層式記錄集中的資料列 (範例) '
title: 存取階層式記錄集中的資料列 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ad70cc527a42188588df31ea7f3a53678423f37d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806718"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>存取階層式記錄集中的資料列 (範例) 
下列範例顯示存取階層式 [記錄集中](../../reference/ado-api/recordset-object-ado.md)的資料列所需的步驟：

1.  **作者**和**titleauthor**資料表中的**記錄集**物件與作者識別碼相關。

2.  外部迴圈會顯示每個作者的名字、姓氏、狀態和識別。

3.  每個資料列的附加 **記錄集會** 從 [Fields](../../reference/ado-api/fields-collection-ado.md) 集合中取出並指派給 *rstTitleAuthor*。

4.  內部迴圈會在附加的 **記錄集中**顯示每個資料列的四個欄位。

 [StayInSync](../../reference/ado-api/stayinsync-property.md)屬性設定為**false** ，以供說明之用，讓您可以在外部迴圈的每個反復專案中明確地查看章節變更。 若要讓程式碼範例更有效率，您可以在步驟3中的第一行之前移動步驟3中的指派，如此一來，指派才會執行一次。 然後，將 [ [StayInSync](../../reference/ado-api/stayinsync-property.md) ] 屬性設定為 [ **true**]，如此一來，每當*rst*移至新的資料列時， *rstTitleAuthor*就會隱含地自動變更為對應的章節。

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
 [資料成形總覽](./data-shaping-overview.md)[欄位物件](../../reference/ado-api/field-object.md)[欄位集合 (ado) ](../../reference/ado-api/fields-collection-ado.md) [正式形式文法](./formal-shape-grammar.md) [Microsoft 資料成形 OLE DB 服務 (Ado 服務提供者](../appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)) [ado (Ado) ](../../reference/ado-api/recordset-object-ado.md)資料成形[圖形附加子句](./shape-append-clause.md)[圖形命令](./shape-commands-in-general.md)的[必要提供者](./required-providers-for-data-shaping.md)一般[圖形計運算元句](./shape-compute-clause.md) [Visual Basic for Applications 函數](./visual-basic-for-applications-functions.md)