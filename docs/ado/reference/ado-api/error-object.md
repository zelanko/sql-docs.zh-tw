---
description: Error 物件
title: Error 物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f243fba25a185025c51fb53c030a360a062ef78
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443970"
---
# <a name="error-object"></a>Error 物件
包含有關與提供者的單一作業相關之資料存取錯誤的詳細資料。  
  
## <a name="remarks"></a>備註  
 涉及 ADO 物件的任何作業都可以產生一或多個提供者錯誤。 當發生每個錯誤時，會將一個或多個**錯誤**物件放在[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[Errors](../../../ado/reference/ado-api/errors-collection-ado.md)集合中。 當另一個 ADO 作業產生錯誤時，會清除 **錯誤** 集合，並將一組新的 **錯誤** 物件放在 **錯誤** 集合中。  
  
> [!NOTE]
>  每個 **錯誤** 物件都代表特定的提供者錯誤，而不是 ADO 錯誤。 ADO 錯誤會公開至執行時間例外狀況處理機制。 例如，在 Microsoft Visual Basic 中，發生 ADO 特定的錯誤時，會觸發 **On error** 事件，並顯示在 **錯誤** 物件中。 如需 ADO 錯誤的完整清單，請參閱 [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) 主題。  
  
 您可以讀取 **錯誤** 物件的屬性，以取得每個錯誤的特定詳細資料，包括下列各項：  
  
-   [Description](../../../ado/reference/ado-api/description-property.md)屬性，其中包含錯誤的文字。 這是預設屬性。  
  
-   [Number](../../../ado/reference/ado-api/number-property-ado.md)屬性，其中包含錯誤常數的**長**整數值。  
  
-   [Source](../../../ado/reference/ado-api/source-property-ado-error.md)屬性，識別引發錯誤的物件。 當您在資料來源的要求之後，當**錯誤**集合中有數個**錯誤**物件時，這特別有用。  
  
-   [SQLState](../../../ado/reference/ado-api/sqlstate-property.md)和[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)屬性，可提供 SQL 資料來源的資訊。  
  
 發生提供者錯誤時，它會放在**連接**物件的**Errors**集合中。 ADO 支援透過單一 ADO 作業傳回多個錯誤，以允許提供者特定的錯誤資訊。 若要在錯誤處理常式中取得這項豐富的錯誤資訊，請使用您所使用之語言或環境的適當錯誤陷印功能，然後使用嵌套迴圈來列舉**錯誤**集合中每個**錯誤**物件的屬性。  
  
> [!NOTE]
>  **Microsoft Visual Basic 和 VBScript 使用者** 如果沒有有效的 **連接** 物件，您將需要從 **錯誤** 物件中取出錯誤資訊。  
  
 就像提供者一樣，ADO 會在進行可能產生新的提供者錯誤的呼叫之前，先清除 **OLE Error Info** 物件。 不過，只有在提供者產生新的錯誤或呼叫[Clear](../../../ado/reference/ado-api/clear-method-ado.md)方法時，才會清除**連接**物件上的**錯誤**集合並填入。  
  
 有些屬性和方法會傳回在**錯誤**集合中顯示為**錯誤**物件的警告，但不會終止程式的執行。 在[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件上呼叫[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法之前，請先：**Connection**物件上的[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法;或者，在**記錄集**物件上設定[Filter](../../../ado/reference/ado-api/filter-property.md)屬性，在**Errors**集合上呼叫**Clear**方法。 如此一來，您就可以讀取**錯誤**集合的[Count](../../../ado/reference/ado-api/count-property-ado.md)屬性來測試傳回的警告。  
  
 **錯誤**物件對腳本而言並不安全。  
  
 本節包含下列主題。  
  
-   [Error 物件屬性、方法和事件](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [ (VC + +) 的 Description、HelpCoNtext、説明、NativeError、Number、Source 和 SQLState 屬性範例 ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [ (ADO) 的 Connection 物件 ](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ (ADO) 收集錯誤 ](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
