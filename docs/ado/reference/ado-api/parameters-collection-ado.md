---
title: 參數集合 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dbfff2a8db4405e19eb448e7bd7db5c8ac236f8
ms.sourcegitcommit: 98324d9803edfa52508b6d5d3554614d0350a0b9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52321794"
---
# <a name="parameters-collection-ado"></a>Parameters 集合 (ADO)
包含所有[參數](../../../ado/reference/ado-api/parameter-object.md)的物件[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
## <a name="remarks"></a>備註  
 A**命令**物件具有**參數**組成的集合**參數**物件。  
  
 使用[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法**命令**物件的**參數**集合擷取提供者的預存程序或參數化的查詢的參數資訊中指定**命令**物件。 某些提供者不支援預存程序呼叫或參數化的查詢;呼叫**重新整理**方法**參數**集合時使用這類提供者會傳回錯誤。  
  
 如果您還沒有定義您自己**參數**物件，並存取**參數**集合，然後再呼叫**重新整理**方法，ADO 會自動會呼叫方法並填入您的集合。  
  
 您可以呼叫提供者來改善效能，如果您知道參數的屬性相關聯的預存程序或參數化查詢您想要呼叫降至最低。 使用  [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法來建立**參數**具有適當的屬性設定和使用物件[附加](../../../ado/reference/ado-api/append-method-ado.md)方法，將其新增至**參數**集合。 這可讓您設定和傳回參數值，而不需要呼叫提供者之參數資訊。 如果您要寫入未提供參數資訊的提供者，您必須手動將填入**參數**使用此方法可以完全使用參數的集合。 使用[刪除](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)方法來移除**參數**物件**參數**如有必要的集合。  
  
 中的物件**參數**的集合**Recordset**移超出範圍 （因此變成無法使用） 時**資料錄集**已關閉。  
  
 呼叫預存程序時**命令**，擷取預存程序的傳回值/輸出參數，如下所示：  
  
1.  呼叫預存程序，沒有任何參數，當**重新整理**方法**參數**呼叫之前，應該呼叫集合**Execute**方法**命令**物件。  
  
2.  當呼叫預存程序使用參數和明確附加的參數**參數**集合**附加**，傳回的值/輸出參數應該附加至**參數**集合。 傳回的值必須先附加至**參數**集合。 使用**Append**新增到其他的參數**參數**定義順序的集合。 例如，預存程序 SPWithParam 有兩個參數。 第一個參數， *InParam*，並輸入的參數定義為 adVarChar (20)，第二個參數， *OutParam*，是一個 output 參數，定義為 adVarChar (20)。 您可以擷取傳回值/輸出參數為下列程式碼。  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOutput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  當呼叫預存程序使用參數和設定的參數，藉由呼叫**項目**方法**參數**集合，預存程序的傳回值/輸出參數可以從擷取**參數**集合。 例如，預存程序 SPWithParam 有兩個參數。 第一個參數， *InParam*，並輸入的參數定義為 adVarChar (20)，第二個參數， *OutParam*，是一個 output 參數，定義為 adVarChar (20)。 您可以擷取傳回值/輸出參數為下列程式碼。  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Item("InParam").value = "hello world" ' input parameter  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of stored procedure  
    ' Access ccmd.parameters(2) or ccmd.parameters("OutParam") as the output parameter.  
    ```  
  
 本章節包含下列主題。  
  
-   [Parameters 集合屬性、 方法和事件](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)
