---
title: 命令物件 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ab3348906affc9a1c1a4b5471de861831992dc32
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47645726"
---
# <a name="command-object-ado"></a>Command 物件 (ADO)
定義您想要執行對資料來源的特定命令。  
  
## <a name="remarks"></a>備註  
 使用**命令**來查詢資料庫，並傳回記錄中的物件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，來執行大量作業，或操作資料庫的結構。 某些功能的提供者，而定**命令**集合、 方法或屬性可能會產生錯誤時參考它們。  
  
 使用集合、 方法和屬性的**命令**物件時，您可以執行下列動作：  
  
-   定義命令 （例如，SQL 陳述式） 的可執行檔的文字[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性。 或者，如命令或查詢結構而非簡單字串 （例如，XML 範本查詢） 會定義使用的指令[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性。  
  
-   （選擇性） 表示中所使用的命令用語**CommandText**或是**CommandStream**具有[方言](../../../ado/reference/ado-api/dialect-property.md)屬性。  
  
-   定義參數化的查詢或預存程序的引數[參數](../../../ado/reference/ado-api/parameter-object.md)物件並[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
-   指出參數名稱是否應傳遞給提供者[NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)屬性。  
  
-   執行命令，並傳回**Recordset**物件，如果具有適當[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
-   指定命令的型別[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)來最佳化效能的執行前的屬性。  
  
-   控制提供者是否儲存已備妥 （或已編譯的） 版本之前使用執行命令[已準備](../../../ado/reference/ado-api/prepared-property-ado.md)屬性。  
  
-   設定提供者會等候命令執行的秒數[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)屬性。  
  
-   將與開啟的連接產生關聯**命令**物件，藉由設定其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性。  
  
-   設定[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性來識別**命令**物件上相關聯的方法作為[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
-   傳遞**命令**物件[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性**資料錄集**取得資料。  
  
-   存取提供者特定屬性，與[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  若要執行查詢，而不使用**命令**物件，傳遞至查詢字串[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法**連接**物件或[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)的方法**資料錄集**物件。 不過，**命令**物件時，需要您想要保存的命令文字和重新執行，或使用查詢參數。  
  
 若要建立**命令**獨立於先前定義的物件**連線**物件，設定其**ActiveConnection**屬性設為有效的連接字串。 仍會建立 ADO**連線**物件，但它不會指派該物件給物件變數。 不過，如果將多個相關聯**命令**物件與相同的連接，您應該明確地建立並開啟**連線**物件; 此指派**連接**給物件變數的物件。 請確定**連接**物件已成功開啟，您將它指派給之前**ActiveConnection**屬性**命令**物件，因為指派關閉**連線**物件會造成錯誤。 如果您未設定**ActiveConnection**屬性**命令**物件給此物件變數，建立新的 ADO**連接**物件給每個**命令**物件，即使您使用相同的連接字串。  
  
 若要執行**命令**，呼叫其[名稱](../../../ado/reference/ado-api/name-property-ado.md)上相關聯的屬性**連接**物件。 **命令**必須要有其**ActiveConnection**屬性設定為**連接**物件。 如果**命令**有參數，將其值做為引數，傳遞至方法。  
  
 如果兩個或以上**命令**物件執行相同的連接並**命令**物件是使用輸出參數的預存程序就會發生錯誤。 若要執行每個**命令**物件，使用個別的連接或中斷連接所有其他**命令**從連接的物件。  
  
 **參數**集合是預設成員**命令**物件。 如此一來，下列兩個程式碼陳述式是相等的。  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   **命令**物件不是安全的。  
  
 本章節包含下列主題。  
  
-   [命令物件屬性、 方法和事件](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [參數集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
