---
title: "Fields 集合 |Microsoft 文件"
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
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ecfc7532761897cddf868dcb617c6eeb5f32bccb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="the-fields-collection"></a>Fields 集合
**欄位**集合是 ADO 的內建集合的其中一個。 集合是已排序的集合的項目可以當做一個單位加以參考。 如需 ADO 集合的詳細資訊，請參閱[ADO 物件模型](../../../ado/guide/data/ado-objects-and-collections.md)。  
  
 **欄位**集合包含**欄位**物件中每個欄位 （資料行）**資料錄集**。 像所有的 ADO 集合，它有**計數**和**項目**屬性，以及**附加**和**重新整理**方法。 它也有**CancelUpdate**，**刪除**，**重新同步處理**，和**更新**不適用於其他 ADO 集合的方法。  
  
## <a name="examining-the-fields-collection"></a>檢查欄位集合  
 請考慮**欄位**的範例集合**資料錄集**引進這一節。 此範例**資料錄集**衍生自 SQL 陳述式  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 因此，您應該會發現**資料錄集欄位**集合包含三個欄位。  
  
```  
'BeginWalkFields  
    Dim objFields As ADODB.Fields  
    Dim intLoop As Integer  
  
    objRs.Open strSQL, strConnStr, adOpenForwardOnly, adLockReadOnly, adCmdText  
  
    Set objFields = objRs.Fields  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
    Next  
'EndWalkFields  
```  
  
 這段程式碼只會決定數目**欄位**中的物件**欄位**集合使用**計數**屬性和集合，傳回的值執行迴圈**名稱**每個屬性**欄位**物件。 您可以使用更多**欄位**屬性來取得欄位的相關資訊。 如需有關查詢**欄位**，請參閱[欄位 Object](../../../ado/guide/data/the-field-object.md)。  
  
## <a name="counting-columns"></a>計算資料行  
 如您所料，**計數**屬性傳回的實際數目**欄位**中的物件**欄位**集合。 因為集合的成員，編號從 0 開始，您應一律撰寫迴圈零的成員開始和結束值是**計數**減 1 的屬性。 如果您使用 Microsoft Visual Basic，而且想要循環集合的成員，而不檢查**計數**屬性，請使用**每個...下一步**命令。  
  
 如果**計數**屬性為零，集合中沒有任何物件。  
  
## <a name="getting-to-the-field"></a>取得欄位  
 如同任何 ADO 集合，**項目**屬性是集合的預設屬性。 它會傳回個別**欄位**名稱所指定的物件或傳遞給它的索引。 因此，下列陳述式是相同範例**資料錄集**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 如果這些方法是對等項目，這是最佳？ 視情況而定。 使用索引來擷取**欄位**從集合，所以更快速存取**欄位**直接而不需要執行字串查閱。 另一方面，順序**欄位**集合內必須知道，而且如果順序變更，以參考**欄位的**索引會有變更，只要它發生。 雖然稍微變慢，但使用的名稱**欄位**是更有彈性，因為它的順序不相依**欄位**集合中。  
  
## <a name="using-the-refresh-method"></a>使用重新整理方法  
 不同於某些其他 ADO 集合，使用**重新整理**方法**欄位**集合具有作用不明顯。 若要從基礎資料庫結構中擷取的變更，您必須使用**Requery**方法，或如果**資料錄集**物件不支援書籤、 **MoveFirst**方法，這會導致一次執行的提供者的命令。  
  
## <a name="adding-fields-to-a-recordset"></a>將欄位加入至資料錄集  
 **附加**方法用來將欄位加入至**資料錄集**。  
  
 您可以使用**附加**方法，以製作**資料錄集**以程式設計的方式而不需要開啟資料來源的連接。 如果會發生執行階段錯誤**附加**上呼叫方法**欄位**的開放集合**資料錄集**或在**資料錄集**其中**ActiveConnection**屬性已設定。 您可以只將附加欄位**資料錄集**，並未開啟，且尚未連接到資料來源。 不過，若要指定新附加的值**欄位**、**資料錄集**第一次必須開啟。  
  
 開發人員通常需要暫時儲存一些資料，或想要某些資料以當做其來源伺服器，才能參與使用者介面中的資料繫結的地方。 ADO (搭配[Microsoft OLE DB 的資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) 可讓開發人員建立空白**資料錄集**物件所指定資料行資訊及呼叫**開啟**. 在下列範例中，三個新的欄位會附加至新**資料錄集**物件。 則**資料錄集**開啟時，兩個新記錄會加入，而**資料錄集**保存至檔案。 (如需有關**資料錄集**持續性，請參閱[正在更新及保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。)  
  
```  
'BeginFabricate  
    Dim objRs As ADODB.Recordset  
    Set objRs = New ADODB.Recordset  
  
    With objRs.Fields  
        .Append "StudentID", adChar, 11, adFldUpdatable  
        .Append "FullName", adVarChar, 50, adFldUpdatable  
        .Append "PhoneNmbr", adVarChar, 20, adFldUpdatable  
    End With  
  
    With objRs  
        .Open  
  
        .AddNew  
        .Fields(0) = "123-45-6789"  
        .Fields(1) = "John Doe"  
        .Fields(2) = "(425) 555-5555"  
        .Update  
  
        .AddNew  
        .Fields(0) = "123-45-6780"  
        .Fields(1) = "Jane Doe"  
        .Fields(2) = "(615) 555-1212"  
        .Update  
    End With  
  
    objRs.Save App.Path & "FabriTest.adtg", adPersistADTG  
  
    objRs.Close  
'EndFabricate  
```  
  
 使用**欄位附加**方法各有不同**資料錄集**物件和**記錄**物件。 如需有關**記錄**物件，請參閱[記錄和資料流](../../../ado/guide/data/records-and-streams.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [產生階層式資料錄集](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
