---
description: AddNew 方法 (ADO)
title: " (ADO) 的 AddNew 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords:
- AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
author: rothja
ms.author: jroth
ms.openlocfilehash: b3c6d6b33177f3c3db7c2d414759a5067a91b80d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451580"
---
# <a name="addnew-method-ado"></a>AddNew 方法 (ADO)
針對可更新的 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件建立新的記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>參數  
 *記錄*  
 **記錄集**物件。  
  
 *FieldList*  
 選擇性。 單一名稱，或是新記錄中欄位的名稱或序數位置陣列。  
  
 *值*  
 選擇性。 單一值，或新記錄中欄位的值陣列。 如果 *Fieldlist* 是陣列， *值* 也必須是具有相同成員數目的陣列;否則，就會發生錯誤。 功能變數名稱的順序必須符合每個陣列中域值的順序。  
  
## <a name="remarks"></a>備註  
 使用 **AddNew** 方法來建立和初始化新的記錄。 使用 [支援](../../../ado/reference/ado-api/supports-method.md) 方法搭配 **adAddNew** ([CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)) 值，以確認是否可以將記錄加入至目前的 **記錄集** 物件。  
  
 在您呼叫 **AddNew** 方法之後，新的記錄會成為目前的記錄，並在您呼叫 [Update](../../../ado/reference/ado-api/update-method.md) 方法之後保持最新狀態。 因為新的記錄會附加至 **記錄集**，所以在更新之後呼叫 **MoveNext** 將會移到 **記錄集**的結尾，並讓 **EOF** 成為 True。 如果 **記錄集** 物件不支援書簽，則在移至另一筆記錄之後，您可能無法存取新的記錄。 視您的資料指標類型而定，您可能需要呼叫 [Requery](../../../ado/reference/ado-api/requery-method.md) 方法來讓新記錄變成可存取。  
  
 如果您在編輯目前的記錄或加入新記錄時呼叫 **AddNew** ，ADO 會呼叫 **Update** 方法來儲存任何變更，然後建立新的記錄。  
  
 **AddNew**方法的行為取決於**記錄集**物件的更新模式，以及您是否傳遞*Fieldlist*和*Values*引數。  
  
 在 *立即更新模式* 中 (當您呼叫 **update** 方法) 時，提供者會將變更寫入基礎資料來源，而不使用引數則呼叫 **AddNew** 方法，會將 [EditMode](../../../ado/reference/ado-api/editmode-property.md) 屬性設定為 **adEditAdd** ([EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) 值) 。 提供者會在本機快取任何域值變更。 呼叫 **Update** 方法會將新記錄張貼至資料庫，並將 **EditMode** 屬性重設為 **adEditNone** (**EditModeEnum** 值) 。 如果您傳遞 *Fieldlist* 和 *Values* 引數，ADO 會立即將新記錄張貼至資料庫， (不需要 **更新** 呼叫) ; **EditMode** 屬性值不會變更 (**adEditNone**) 。  
  
 在 *批次更新模式* (中，提供者會快取多個變更，並將它們寫入基礎資料來源，只有當您呼叫 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 方法) 時，呼叫不含引數的 **AddNew** 方法會將 **EditMode** 屬性設定為 **adEditAdd**。 提供者會在本機快取任何域值變更。 呼叫 **Update** 方法會將新的記錄加入目前的 **記錄集**，但是提供者不會將變更張貼到基礎資料庫，或將 **EditMode** 重設為 **adEditNone**，直到您呼叫 **UpdateBatch** 方法為止。 如果您傳遞 *Fieldlist* 和 *Values* 引數，ADO 會將新記錄傳送給提供者，以便在快取中儲存，並將 **EditMode** 設定為 **adEditAdd**;您必須呼叫 **UpdateBatch** 方法，以將新記錄張貼到基礎資料庫。  
  
## <a name="example"></a>範例  
 下列範例顯示如何使用 AddNew 方法搭配包含的欄位清單和值清單，以瞭解如何將欄位清單和值清單包含為數組。  
  
```  
create table aa1 (intf int, charf char(10))  
insert into aa1 values (2, 'aa')  
  
Dim cn As New adodb.Connection  
Dim rs As New adodb.Recordset  
Dim cmd As New adodb.Command  
  
cn.ConnectionString = "Provider=SQLOLEDB;Data Source=alexverb2;uid=sa;pwd=foo$bar00;"  
  
cn.Open  
rs.Open "select * from xxx..aa1", cn, adOpenKeyset, adLockOptimistic  
  
Dim fieldsArray(1) As Variant  
fieldsArray(0) = "intf"  
fieldsArray(1) = "charf"  
Dim values(1) As Variant  
values(0) = 4  
values(1) = "as"  
rs.AddNew fieldsArray, values  
rs.Update  
```  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的 AddNew 方法範例) ](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [AddNew 方法範例 (VBScript) ](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [ (VC + +) 的 AddNew 方法範例 ](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [ (ADO) 的 CancelUpdate 方法 ](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 屬性](../../../ado/reference/ado-api/editmode-property.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)   
 [支援方法](../../../ado/reference/ado-api/supports-method.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
