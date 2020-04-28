---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e73b2ca96cc5e7eb7683b72aa19fd59a318b8596
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926350"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>存取階層式記錄集中的資料列（範例）
下列範例顯示存取階層式[記錄集中](../../../ado/reference/ado-api/recordset-object-ado.md)的資料列所需的步驟：

1.  **作者**和**titleauthor**資料表中的**記錄集**物件是由作者識別碼所關聯。

2.  外部迴圈會顯示每位作者的名字和姓氏、狀態和識別。

3.  每個資料列的附加**記錄集會**從[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合抓取並指派給*rstTitleAuthor*。

4.  內部迴圈會顯示附加之**記錄集中**每個資料列的四個欄位。

 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)屬性會設定為**false** ，供說明之用，讓您可以看到外部迴圈的每個反復專案中明確變更的章節。 若要讓程式碼範例更有效率，您可以將步驟3中的指派移到步驟2中的第一行之前，讓指派只執行一次。 然後將[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)屬性設定為**true**，如此一來，每當*rst*移到新的資料列時， *rstTitleAuthor*就會隱含並自動變更為對應的章節。

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
 [資料成形總覽](../../../ado/guide/data/data-shaping-overview.md)[欄位物件](../../../ado/reference/ado-api/field-object.md)[欄位集合（ado）](../../../ado/reference/ado-api/fields-collection-ado.md) [正式圖形文法](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft 資料成形服務適用于 OLE DB （ado 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [Recordset 物件（ado）](../../../ado/reference/ado-api/recordset-object-ado.md) [在一般](../../../ado/guide/data/shape-commands-in-general.md)[形狀計運算元句](../../../ado/guide/data/shape-compute-clause.md)中[，資料成形](../../../ado/guide/data/required-providers-for-data-shaping.md)[圖形 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)圖形命令的必要提供者[Visual Basic for Applications 函數](../../../ado/guide/data/visual-basic-for-applications-functions.md)
