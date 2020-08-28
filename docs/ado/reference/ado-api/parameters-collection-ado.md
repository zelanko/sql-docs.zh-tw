---
description: Parameters 集合 (ADO)
title: " (ADO) 的參數集合 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: bad2570c368e469afeb7c69e4f283bdbdfe04674
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990119"
---
# <a name="parameters-collection-ado"></a>Parameters 集合 (ADO)
包含[Command](./command-object-ado.md)物件的所有[參數](./parameter-object.md)物件。  
  
## <a name="remarks"></a>備註  
 **命令**物件具有由**參數**物件組成的**參數**集合。  
  
 在**命令**物件的**Parameters**集合上使用[Refresh](./refresh-method-ado.md)方法，會抓取**命令**物件中所指定預存程式或參數化查詢的提供者參數資訊。 有些提供者不支援預存程序呼叫或參數化查詢;使用這類提供者時，在**參數**集合上呼叫**Refresh**方法將會傳回錯誤。  
  
 如果您尚未定義您自己的**參數**物件，且在呼叫**Refresh**方法之前存取了**Parameters**集合，則 ADO 會自動呼叫方法並為您填入集合。  
  
 如果您知道與您想要呼叫之預存程式或參數化查詢相關聯之參數的屬性，您可以儘量減少對提供者的呼叫，以改善效能。 您可以使用 [CreateParameter](./createparameter-method-ado.md) 方法，以適當的屬性設定來建立 **參數** 物件，並使用 [Append](./append-method-ado.md) 方法將它們加入至 **Parameters** 集合。 這可讓您設定和傳回參數值，而不需要呼叫提供者取得參數資訊。 如果您要寫入未提供參數資訊的提供者，則必須使用此方法手動填入 **參數** 集合，才能使用參數。 如有必要，請使用[Delete](./delete-method-ado-parameters-collection.md)方法，從**Parameters**集合中移除**參數**物件。  
  
 **記錄集**之**Parameters**集合中的物件會移出範圍 (因此，在關閉**記錄集**時變成無法使用的) 。  
  
 使用 **命令**呼叫預存程式時，預存程式的傳回值/輸出參數會依照下列方式進行取出：  
  
1.  呼叫沒有參數的預存程式時，應在呼叫**Command**物件的**Execute**方法之前，先呼叫**parameters**集合上的**Refresh**方法。  
  
2.  使用**附加**參數來呼叫預存程式並明確地將參數附加至**parameters**集合時，傳回值/輸出參數應附加至**parameters**集合。 傳回值必須先附加至 **Parameters** 集合。 使用 [ **附加** ]，以定義的順序將其他參數加入至 **參數** 集合。 例如，預存程式 SPWithParam 有兩個參數。 第一個參數 *InParam*是定義為 adVarChar (20) 的輸入參數，而第二個參數 *OutParam*是定義為 adVarChar (20) 的輸出參數。 您可以使用下列程式碼來取得傳回值/輸出參數。  
  
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
  
3.  當您呼叫具有參數的預存程式，並透過呼叫**parameters**集合上的**Item**方法來設定參數時，可以從**parameters**集合中取出預存程式的傳回值/輸出參數。 例如，預存程式 SPWithParam 有兩個參數。 第一個參數 *InParam*是定義為 adVarChar (20) 的輸入參數，而第二個參數 *OutParam*是定義為 adVarChar (20) 的輸出參數。 您可以使用下列程式碼來取得傳回值/輸出參數。  
  
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
  
 本節包含下列主題。  
  
-   [Parameters 集合屬性、方法和事件](./parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 Append 方法 ](./append-method-ado.md)   
 [ (ADO) 的 CreateParameter 方法 ](./createparameter-method-ado.md)   
 [Parameter 物件](./parameter-object.md)