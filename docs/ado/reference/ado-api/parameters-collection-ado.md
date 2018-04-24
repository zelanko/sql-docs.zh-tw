---
title: 參數集合 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e6557489b5051a7d92864b662b1822b9e6d0dff4
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="parameters-collection-ado"></a>參數集合 (ADO)
包含所有[參數](../../../ado/reference/ado-api/parameter-object.md)物件[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
## <a name="remarks"></a>備註  
 A**命令**物件具有**參數**集合組成**參數**物件。  
  
 使用[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法**命令**物件的**參數**集合擷取提供者的預存程序或參數化的查詢的參數資訊指定在**命令**物件。 某些提供者不支援預存程序呼叫或參數化的查詢。呼叫**重新整理**方法**參數**集合時使用這類提供者會傳回錯誤。  
  
 如果您還沒有定義您自己**參數**物件，以及存取**參數**集合，然後再呼叫**重新整理**自動呼叫方法時，ADO 會方法，並填入您的集合。  
  
 您可以呼叫提供者來改善效能，如果預存程序相關聯的參數屬性，或參數化查詢，您知道您想要呼叫降至最低。 使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法來建立**參數**具有適當的屬性設定和使用物件[附加](../../../ado/reference/ado-api/append-method-ado.md)方法將其新增至**參數**集合。 這可讓您設定和傳回參數值，而不必呼叫提供者之參數資訊。 如果您要寫入的提供者，並不提供參數資訊，您必須手動將填入**參數**使用這個方法無法完全使用參數的集合。 使用[刪除](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)方法移除**參數**物件從**參數**如有必要的集合。  
  
 中的物件**參數**集合**資料錄集**超出範圍 （因此變成無法使用） 時**資料錄集**已關閉。  
  
 呼叫預存程序時**命令**，擷取預存程序的傳回值/輸出參數，如下所示：  
  
1.  當呼叫預存程序，沒有任何參數，**重新整理**方法**參數**集合應該會在呼叫之前呼叫**Execute**方法**命令**物件。  
  
2.  當呼叫預存程序使用參數和明確附加到參數**參數**集合**附加**，傳回值/輸出參數應該附加至**參數**集合。 傳回值必須先附加至**參數**集合。 使用**附加**來加入其他參數到**參數**以定義順序的集合。 例如，預存程序 SPWithParam 有兩個參數。 第一個參數， *InParam*，是輸入的參數定義為 adVarChar (20)，而第二個參數*OutParam*，是一個 output 參數，定義為 adVarChar (20)。 您可以擷取下列程式碼的傳回值/輸出參數。  
  
    ```  
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOuput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  當呼叫預存程序使用參數和設定的參數，藉由呼叫**項目**方法**參數**集合，預存程序的傳回值/輸出參數可以從擷取**參數**集合。 例如，預存程序 SPWithParam 有兩個參數。 第一個參數， *InParam*，是輸入的參數定義為 adVarChar (20)，而第二個參數*OutParam*，是一個 output 參數，定義為 adVarChar (20)。 您可以擷取下列程式碼的傳回值/輸出參數。  
  
    ```  
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
  
-   [參數集合的屬性、 方法和事件](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)
