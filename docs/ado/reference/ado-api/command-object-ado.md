---
title: Command 物件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbce299e2e9f67b705f940480913c7d8ac367d0d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919791"
---
# <a name="command-object-ado"></a>Command 物件 (ADO)
定義您想要針對資料來源執行的特定命令。  
  
## <a name="remarks"></a>備註  
 使用**Command**物件來查詢資料庫，並傳回記錄[集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中的記錄、執行大量作業，或運算元據庫的結構。 視提供者的功能而定，某些**命令**集合、方法或屬性在被參考時可能會產生錯誤。  
  
 透過**命令**物件的集合、方法和屬性，您可以執行下列動作：  
  
-   使用[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性定義命令的可執行檔文字（例如 SQL 語句）。 或者，對於簡單字串以外的命令或查詢結構（例如，XML 範本查詢），會使用[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性來定義命令。  
  
-   （選擇性）在**CommandText**或**CommandStream**中，使用[方言](../../../ado/reference/ado-api/dialect-property.md)屬性來表示命令方言。  
  
-   使用[參數](../../../ado/reference/ado-api/parameter-object.md)物件和[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合來定義參數化查詢或預存程式引數。  
  
-   指出是否應該使用[NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)屬性，將參數名稱傳遞給提供者。  
  
-   執行命令，並在適當時傳回**記錄集**物件，以[執行](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
-   在執行之前，使用[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性指定命令的類型，以優化效能。  
  
-   控制提供者是否會在執行[備](../../../ado/reference/ado-api/prepared-property-ado.md)妥的屬性之前，先儲存已備妥（或已編譯）的命令版本。  
  
-   設定提供者將使用[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)屬性來等候命令執行的秒數。  
  
-   藉由設定其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性，讓開啟的連接與**命令**物件產生關聯。  
  
-   設定 [[名稱](../../../ado/reference/ado-api/name-property-ado.md)] 屬性，將**命令**物件識別為相關聯[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件上的方法。  
  
-   將**命令**物件傳遞至**記錄集**的[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性，以取得資料。  
  
-   使用[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合存取提供者特有的屬性。  
  
> [!NOTE]
>  若要在不使用**Command**物件的情況下執行查詢，請將查詢字串傳遞至**連接**物件的[execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法或**記錄集**物件的[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。 不過，當您想要保存命令文字並重新執行它，或使用查詢參數時，需要**command**物件。  
  
 若要建立與先前定義的**連接**物件無關的**命令**物件，請將其**ActiveConnection**屬性設為有效的連接字串。 ADO 仍然會建立**連接**物件，但不會將該物件指派給物件變數。 不過，如果您要將多個**命令**物件與相同的連接產生關聯，您應該明確地建立並開啟**連接**物件;這會將**連接**物件指派給物件變數。 請先確定**連接**物件已成功開啟，再將它指派給**Command**物件的**ActiveConnection**屬性，因為指派已關閉的**連接**物件會造成錯誤。 如果您未將**Command**物件的**ActiveConnection**屬性設定為這個物件變數，ADO 就會為每個**命令**物件建立新的**連接**物件，即使您使用相同的連接字串也一樣。  
  
 若要執行**命令**，請在相關聯的**連接**物件上呼叫它的[Name](../../../ado/reference/ado-api/name-property-ado.md)屬性。 此**命令**的**ActiveConnection**屬性必須設定為**Connection**物件。 如果**命令**有參數，請將其值當做引數傳遞給方法。  
  
 如果在相同的連接上執行兩個或多個**命令**物件，且其中一個**命令**物件是具有輸出參數的預存程式，則會發生錯誤。 若要執行每個**命令**物件，請使用個別的連線，或中斷連線中所有其他**命令**物件的連接。  
  
 **Parameters**集合是**Command**物件的預設成員。 因此，下列兩個程式碼語句是相等的。  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   **命令**物件不安全，無法進行腳本處理。  
  
 本章節包含下列主題。  
  
-   [Command 物件屬性、方法和事件](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Connection 物件（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Parameters 集合（ADO）](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
