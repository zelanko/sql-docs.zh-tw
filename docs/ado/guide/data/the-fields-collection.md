---
title: Fields 集合 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 197a57b8a9b9ea2927a057733992a02c731a335a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923931"
---
# <a name="the-fields-collection"></a>Fields 集合
**Fields**集合是 ADO 的內部集合之一。 集合是一組已排序的專案，可以稱為「單位」（unit）。 如需 ADO 集合的詳細資訊，請參閱[Ado 物件模型](../../../ado/guide/data/ado-objects-and-collections.md)。  
  
 **Fields**集合包含**記錄集**內每個欄位（資料行）的**欄位**物件。 就像所有 ADO 集合一樣，它具有**Count**和**Item**屬性，以及**Append**和**Refresh**方法。 此外，它也具有**CancelUpdate**、 **Delete**、 **Resync**和**Update**方法，無法供其他 ADO 集合使用。  
  
## <a name="examining-the-fields-collection"></a>檢查 Fields 集合  
 請考慮本節中所引進之範例**記錄集**的**Fields**集合。 範例**記錄集**衍生自 SQL 語句  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 因此，您應該會發現「**記錄集欄位**」集合包含三個欄位。  
  
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
  
 這段程式碼只會使用**Count**屬性來判斷**Fields**集合中的**欄位**物件數目，並在集合中執行迴圈，傳回每個**Field**物件的**Name**屬性值。 您可以使用多個**欄位**屬性來取得欄位的相關資訊。 如需有關查詢**欄位**的詳細資訊，請參閱[field 物件](../../../ado/guide/data/the-field-object.md)。  
  
## <a name="counting-columns"></a>計算資料行  
 如您所預期， **Count**屬性會傳回**Fields**集合中的**欄位**物件實際數目。 因為集合成員的編號是以零開始，所以您應該一律以零成員開頭的程式碼，並以**Count**屬性的值減1來結束。 如果您使用 Microsoft Visual Basic，而且想要對集合的成員執行迴圈，而不檢查**Count**屬性，請使用**For each .。。下一個**命令。  
  
 如果**Count**屬性為零，則集合中沒有任何物件。  
  
## <a name="getting-to-the-field"></a>取得欄位  
 如同任何 ADO 集合， **Item**屬性是集合的預設屬性。 它會傳回由傳遞給它的名稱或索引所指定的個別**欄位**物件。 因此，下列語句對範例**記錄集**而言是相等的：  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 如果這些方法是相等的，這是最佳的做法？ 這要看狀況。 使用索引從集合中抓取**欄位**的速度較快，因為它會直接存取**欄位**，而不需要執行字串查閱。 另一方面，集合中的**欄位**順序必須是已知的，而且如果順序變更，則**欄位**索引的參考就必須在其發生的位置變更。 雖然稍微慢一點，但使用**欄位**的名稱會更有彈性，因為它不會相依于集合中的**欄位**順序。  
  
## <a name="using-the-refresh-method"></a>使用 Refresh 方法  
 不同于其他 ADO 集合，在**Fields**集合上使用**Refresh**方法不會顯示任何效果。 若要從基礎資料庫結構中抓取變更，您必須使用**Requery**方法，或者，如果**記錄集**物件不支援書簽，則**MoveFirst**方法會導致再次對提供者執行命令。  
  
## <a name="adding-fields-to-a-recordset"></a>將欄位加入至記錄集  
 **Append**方法是用來將欄位加入至**記錄集**。  
  
 您可以使用**Append**方法，以程式設計方式製作**記錄集**，而不需開啟資料來源的連接。 如果在開啟的**記錄集**的**Fields**集合或已設定**ActiveConnection**屬性的**記錄集**上呼叫**Append**方法，就會發生執行階段錯誤。 您只能將欄位附加至尚未開啟且尚未連接至資料來源的**記錄集**。 不過，若要指定新附加**欄位**的值，必須先開啟**記錄集**。  
  
 開發人員通常需要一個位置來暫時儲存一些資料，或想要讓某些資料如同來自伺服器，讓它可以參與使用者介面中的資料系結。 ADO （與[適用于 OLE DB 的 Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)）可讓開發人員藉由指定資料行資訊並呼叫**Open**來建立空的**記錄集**物件。 在下列範例中，會將三個新的欄位附加至新的**記錄集**物件。 然後會開啟**記錄集**、加入兩個新的記錄，並將**記錄集**保存至檔案。 （如需**記錄集**持續性的詳細資訊，請參閱[更新和保存資料](../../../ado/guide/data/updating-and-persisting-data.md)）。  
  
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
  
 **欄位附加**方法的使用方式在**記錄集**物件和**記錄**物件之間有所不同。 如需**記錄**物件的詳細資訊，請參閱[記錄和資料流程](../../../ado/guide/data/records-and-streams.md)。  
  
## <a name="see-also"></a>另請參閱  
 [產生階層式資料錄集](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
