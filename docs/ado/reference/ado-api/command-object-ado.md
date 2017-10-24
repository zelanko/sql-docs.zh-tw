---
title: "命令物件 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 863c922dce68f5e3108136baf90ebc5a3d0b697a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="command-object-ado"></a>命令物件 (ADO)
定義您想要執行對資料來源的特定命令。  
  
## <a name="remarks"></a>備註  
 使用**命令**來查詢資料庫，並傳回記錄中的物件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件來執行大量作業，或操作資料庫的結構。 功能的提供者，根據一些**命令**集合、 方法或屬性可能會產生錯誤時參考它們。  
  
 使用集合、 方法和屬性的**命令**物件，您可以執行下列：  
  
-   定義命令 （例如，SQL 陳述式） 的可執行檔的文字與[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性。 或者，命令或查詢結構而不是簡單的字串 （例如，XML 範本查詢） 會定義與命令[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性。  
  
-   （選擇性） 表示中使用的命令方言**CommandText**或**CommandStream**與[方言](../../../ado/reference/ado-api/dialect-property.md)屬性。  
  
-   定義參數化的查詢或預存程序的引數[參數](../../../ado/reference/ado-api/parameter-object.md)物件和[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
-   指出參數名稱是否應該傳遞到提供者， [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)屬性。  
  
-   執行命令，並傳回**資料錄集**物件具有適當[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
-   指定的命令類型[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性，再執行，以最佳化效能。  
  
-   控制提供者是否儲存之前執行命令的已備妥 （或編譯） 版本[已準備](../../../ado/reference/ado-api/prepared-property-ado.md)屬性。  
  
-   設定提供者會等候命令執行的秒數[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)屬性。  
  
-   建立與開啟的連接關聯**命令**物件藉由設定其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性。  
  
-   設定[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性來識別**命令**物件上相關聯的方法為[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
-   傳遞**命令**物件[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性**資料錄集**取得資料。  
  
-   存取提供者特有的屬性與[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  若要執行查詢，而不使用**命令**物件，傳遞查詢字串以[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法**連接**物件或[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**資料錄集**物件。 不過，**命令**物件時，需要您想要保存的命令文字，並重新執行它，或使用查詢參數。  
  
 若要建立**命令**獨立先前定義的物件**連接**物件、 設定其**ActiveConnection**屬性設為有效的連接字串。 ADO 仍會建立**連接**物件，但它不會指派該物件給物件變數。 不過，如果您要產生多個關聯**命令**物件與相同的連接，您應該明確地建立及開啟**連接**物件; 此指派**連接**給物件變數的物件。 請確定**連接**物件之前，您將它指派給已成功開啟**ActiveConnection**屬性**命令**物件，因為指派關閉**連接**物件會造成錯誤。 如果您未設定**ActiveConnection**屬性**命令**物件給這個物件變數，建立新的 ADO**連接**物件給每個**命令**物件，即使您使用相同的連接字串。  
  
 若要執行**命令**，呼叫其[名稱](../../../ado/reference/ado-api/name-property-ado.md)上相關聯的屬性**連接**物件。 **命令**必須要有其**ActiveConnection**屬性設定為**連接**物件。 如果**命令**有參數，將其值做為引數傳遞至方法。  
  
 如果兩個或多個**命令**物件在相同的連接，然後執行**命令**物件是使用輸出參數的預存程序就會發生錯誤。 若要執行每個**命令**物件、 使用個別的連接或中斷所有其他**命令**從連接物件。  
  
 **參數**集合是預設成員**命令**物件。 因此，下列兩個程式碼陳述式是相等的。  
  
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
 [附錄 a： 提供者](../../../ado/guide/appendixes/appendix-a-providers.md)

