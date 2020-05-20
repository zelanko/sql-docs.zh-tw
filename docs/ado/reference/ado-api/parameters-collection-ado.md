---
title: Parameters 集合（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e087c769fe84e79ca9a41c33912f150249ab2cd9
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763389"
---
# <a name="parameters-collection-ado"></a>Parameters 集合 (ADO)
包含[Command](../../../ado/reference/ado-api/command-object-ado.md)物件的所有[參數](../../../ado/reference/ado-api/parameter-object.md)物件。  
  
## <a name="remarks"></a>備註  
 **命令**物件具有由**參數**物件所組成的**Parameters**集合。  
  
 在**命令**物件的**Parameters**集合上使用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，會抓取**命令**物件中指定之預存程式或參數化查詢的提供者參數資訊。 有些提供者不支援預存程序呼叫或參數化查詢;使用這類提供者時，在**參數**集合上呼叫**Refresh**方法將會傳回錯誤。  
  
 如果您尚未定義自己的**參數**物件，並在呼叫**Refresh**方法之前存取**Parameters**集合，ADO 會自動呼叫方法並為您填入集合。  
  
 如果您知道與您想要呼叫的預存程式或參數化查詢相關聯的參數屬性，則可以將對提供者的呼叫降至最低以改善效能。 使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法來建立具有適當屬性設定的**參數**物件，並使用[Append](../../../ado/reference/ado-api/append-method-ado.md)方法將它們新增至**Parameters**集合。 這可讓您設定和傳回參數值，而不需要為參數資訊呼叫提供者。 如果您要寫入未提供參數資訊的提供者，您必須使用這個方法來手動填入**參數**集合，以便能夠使用參數。 如有需要，請使用[Delete](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)方法從**Parameters**集合中移除**參數**物件。  
  
 當**記錄集**已關閉時，**記錄集**的**Parameters**集合中的物件會移出範圍（因此變成無法使用）。  
  
 使用**命令**呼叫預存程式時，會抓取預存程式的傳回值/輸出參數，如下所示：  
  
1.  呼叫沒有參數的預存程式時，應該先呼叫**parameters**集合上的**Refresh**方法，再呼叫**Command**物件上的**Execute**方法。  
  
2.  呼叫具有參數的預存程式，並使用**Append**將參數明確附加至**parameters**集合時，傳回值/輸出參數應附加至**parameters**集合。 傳回值必須先附加至**Parameters**集合。 使用 [**附加**]，依定義的順序，將其他參數新增至**parameters**集合。 例如，預存程式 SPWithParam 有兩個參數。 第一個參數*InParam*是定義為 adVarChar （20）的輸入參數，而第二個參數*OutParam*是定義為 adVarChar （20）的輸出參數。 您可以使用下列程式碼來抓取傳回值/輸出參數。  
  
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
  
3.  當呼叫具有參數的預存程式，以及在**參數**集合上呼叫**Item**方法來設定參數時，可以從**parameters**集合中抓取預存程式的傳回值/輸出參數。 例如，預存程式 SPWithParam 有兩個參數。 第一個參數*InParam*是定義為 adVarChar （20）的輸入參數，而第二個參數*OutParam*是定義為 adVarChar （20）的輸出參數。 您可以使用下列程式碼來抓取傳回值/輸出參數。  
  
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
  
-   [Parameters 集合屬性、方法和事件](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Append 方法（ADO）](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter 方法（ADO）](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)
