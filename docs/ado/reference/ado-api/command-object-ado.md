---
description: Command 物件 (ADO)
title: " (ADO) 的命令物件 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 252a59f63c4ce782a915a1e1cf11af58fd2f233b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975229"
---
# <a name="command-object-ado"></a>Command 物件 (ADO)
定義您想要對資料來源執行的特定命令。  
  
## <a name="remarks"></a>備註  
 您可以使用 **命令** 物件來查詢資料庫，並傳回記錄 [集](./recordset-object-ado.md) 物件中的記錄、執行大量作業，或是運算元據庫的結構。 視提供者的功能而定，某些 **命令** 集合、方法或屬性在參考時可能會產生錯誤。  
  
 使用 **命令** 物件的集合、方法和屬性，您可以執行下列動作：  
  
-   定義命令的可執行文字 (例如，使用 [CommandText](./commandtext-property-ado.md) 屬性) 的 SQL 語句。 或者，針對簡單字串以外的命令或查詢結構 (例如，XML 範本查詢) 使用 [CommandStream](./commandstream-property-ado.md) 屬性來定義命令。  
  
-   （選擇性）使用 [[方言](./dialect-property.md)] 屬性工作表示**CommandText**或**CommandStream**中所使用的命令方言。  
  
-   使用 [參數](./parameter-object.md) 物件和 [Parameters](./parameters-collection-ado.md) 集合來定義參數化查詢或預存程式引數。  
  
-   指出是否應該使用 [NamedParameters](./namedparameters-property-ado.md) 屬性將參數名稱傳遞給提供者。  
  
-   執行命令並傳回 **記錄集** 物件（如果適用于 [Execute](./execute-method-ado-command.md) 方法的話）。  
  
-   在執行之前，以 [CommandType](./commandtype-property-ado.md) 屬性指定命令類型，以優化效能。  
  
-   使用 [備](./prepared-property-ado.md) 妥的屬性來控制提供者是否要在執行之前儲存備妥的 (或編譯) 版本的命令。  
  
-   設定提供者將使用 [CommandTimeout](./commandtimeout-property-ado.md) 屬性等候命令執行的秒數。  
  
-   藉由設定[ActiveConnection](./activeconnection-property-ado.md)屬性，將開啟的連接與**命令**物件產生關聯。  
  
-   設定 [Name](./name-property-ado.md) 屬性，將 **命令** 物件識別為相關聯 [連接](./connection-object-ado.md) 物件上的方法。  
  
-   將**命令**物件傳遞至**記錄集**的[來源](./source-property-ado-recordset.md)屬性以取得資料。  
  
-   使用 [屬性](./properties-collection-ado.md) 集合存取提供者特有的屬性。  
  
> [!NOTE]
>  若要在不使用**Command**物件的情況下執行查詢，請將查詢字串傳遞至**連接**物件的[execute](./execute-method-ado-connection.md)方法或**記錄集**物件的[Open](./open-method-ado-recordset.md)方法。 但是，當您想要保存命令文字並重新執行它，或使用查詢參數時，需要 **command** 物件。  
  
 若要建立與先前定義之**連接**物件無關的**命令**物件，請將其**ActiveConnection**屬性設定為有效的連接字串。 ADO 仍會建立 **連接** 物件，但不會將該物件指派給物件變數。 但是，如果您要將多個 **命令** 物件與相同的連接產生關聯，您應該明確建立並開啟 **連接** 物件;這會將 **連接** 物件指派給物件變數。 將連線物件指派給**Command**物件的**ActiveConnection**屬性之前，請確定已成功開啟**連接**物件，因為指派封閉的**連接**物件會導致錯誤。 如果您未將**命令**物件的**ActiveConnection**屬性設定為此物件變數，則 ADO 會為每個**命令**物件建立新的**連接**物件，即使您使用相同的連接字串也是如此。  
  
 若要執行**命令**，請在相關聯的**連接**物件上呼叫它的[Name](./name-property-ado.md)屬性。 **命令**的**ActiveConnection**屬性必須設定為**Connection**物件。 如果 **命令** 有參數，請將其值以引數的形式傳遞給方法。  
  
 如果在相同的連接上執行兩個以上的 **命令** 物件，而且其中一個 **命令** 物件是具有 output 參數的預存程式，則會發生錯誤。 若要執行每個 **命令** 物件，請使用不同的連接，或中斷連接的所有其他 **命令** 物件。  
  
 **Parameters**集合是**Command**物件的預設成員。 因此，下列兩個程式碼語句是相等的。  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   **命令**物件對腳本而言並不安全。  
  
 本節包含下列主題。  
  
-   [Command 物件屬性、方法和事件](./command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 Connection 物件 ](./connection-object-ado.md)   
 [ (ADO) 的參數集合 ](./parameters-collection-ado.md)   
 [ (ADO) 的屬性集合 ](./properties-collection-ado.md)   
 [附錄 A：提供者](../../guide/appendixes/appendix-a-providers.md)