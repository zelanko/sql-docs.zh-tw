---
title: 命令參數 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- parameters [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, parameters
- SQL Server Native Client OLE DB provider, commands
- parameters [SQL Server Native Client], OLE DB
- commands [OLE DB]
ms.assetid: 072ead49-ebaf-41eb-9a0f-613e9d990f26
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5db24ee3b68d1a8989200479a3ce4018e63a5177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304508"
---
# <a name="command-parameters"></a>命令參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在命令文字中，參數會以問號字元來標示。 例如，下列 SQL 陳述式是針對單一輸入參數標示：  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 為了透過減少網路流量來提高性能,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式不會自動派生參數資訊,除非在執行命令之前調用**ICommand 與參數::獲取參數資訊**或**ICommandPrepare::P重新資料。** 這意味著[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE 資料庫提供者不會自動:  
  
-   確認使用 **ICommandWithParameters::SetParameterInfo** 所指定之資料類型的正確性。  
  
-   從存取子繫結資訊中指定的 DBTYPE 對應至參數的正確 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
 如果應用程式指定了與參數之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型不相容的資料類型，它們將在使用其中一種方法時收到可能的錯誤或遺失有效位數。  
  
 若要確保不會發生這種情況，應用程式應該：  
  
-   確定 *pwszDataSourceType* 符合參數的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型 (如果寫入 **ICommandWithParameters::SetParameterInfo** 程式碼的話)。  
  
-   確定繫結至參數的 DBTYPE 值與參數的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型具有相同的類型 (如果寫入存取子程式碼的話)。  
  
-   將應用程式編碼成呼叫 **ICommandWithParameters::GetParameterInfo**，如此提供者就可以用動態方式取得參數的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 請注意，這可能會導致與伺服器之間的額外網路往返。  
  
> [!NOTE]  
>  在下列情況下，提供者不支援呼叫 **ICommandWithParameters::GetParameterInfo**：包含 FROM 子句的任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UPDATE 或 DELETE 陳述式、相依於包含參數之子查詢的任何 SQL 陳述式、在比較 (like) 或定量述詞的運算式中都包含參數標記的 SQL 陳述式，或是其中一個參數為函式參數的任何查詢。 在處理 SQL 陳述式批次時，提供者也不支援針對批次內第一個陳述式之後的陳述式中的參數標記呼叫 **ICommandWithParameters::GetParameterInfo**。 不允許在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令中使用註解 (/* \*/)。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供者支援 SQL 語句命令中的輸入參數。 在程序呼叫指令上,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式支援輸入、輸出和輸入/輸出參數。 在執行 (只有在沒有傳回任何資料列集時) 或應用程式已用盡所有傳回的資料列集時，輸出參數值就會傳回應用程式。 若要確保傳回的值有效，請使用 **IMultipleResults** 來強制資料列集取用。  
  
 您不需要在 DBPARAMBINDINFO 結構中指定預存程序參數的名稱。 對*pwszName*成員的值使用 NULL 以指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式應忽略參數名稱,並且僅使用 ICommand 與參數的*rgParamOrdinals*成員中指定的表位 **::set參數資訊**。 如果命令文字同時包含已命名和未命名的參數，您就必須在任何已命名的參數前面指定所有未命名的參數。  
  
 如果指定了儲存過程參數的名稱,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式將檢查該名稱以確保其有效。 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式在從消費者收到錯誤的參數名稱時返回錯誤。  
  
> [!NOTE]  
>  為了公開對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和使用者定義類型 (UDT)[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的支援,本機用戶端 OLE DB 提供程式實現了一個新的[ISSCommand 與參數介面](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
