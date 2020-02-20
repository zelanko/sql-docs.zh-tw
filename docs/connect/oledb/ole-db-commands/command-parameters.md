---
title: 命令參數 | Microsoft Docs
description: 命令參數
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- parameters [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, parameters
- OLE DB Driver for SQL Server, commands
- parameters [OLE DB Driver for SQL Server], OLE DB
- commands [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 1ed49ebaffb46b8542247e67ff7c639cec1cca1d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68016112"
---
# <a name="command-parameters"></a>命令參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在命令文字中，參數會以問號字元來標示。 例如，下列 SQL 陳述式是針對單一輸入參數標示：  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 為了透過減少網路傳輸來改善效能，除非在執行命令之前呼叫了 **ICommandWithParameters::GetParameterInfo** 或 **ICommandPrepare::Prepare**，否則 OLE DB Driver for SQL Server 不會自動衍生參數資訊。 這表示 OLE DB Driver for SQL Server 不會自動：  
  
-   確認使用 **ICommandWithParameters::SetParameterInfo** 所指定之資料類型的正確性。  
  
-   從存取子繫結資訊中指定的 DBTYPE 對應至參數的正確 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。  
  
 如果應用程式指定了與參數之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型不相容的資料類型，它們將在使用其中一種方法時收到可能的錯誤或遺失有效位數。  
  
 若要確保不會發生這種情況，應用程式應該：  
  
-   確定 *pwszDataSourceType* 符合參數的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型 (如果寫入 **ICommandWithParameters::SetParameterInfo** 程式碼的話)。  
  
-   確定繫結至參數的 DBTYPE 值與參數的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型具有相同的類型 (如果寫入存取子程式碼的話)。  
  
-   將應用程式編碼成呼叫 **ICommandWithParameters::GetParameterInfo**，如此提供者就可以用動態方式取得參數的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。 請注意，這可能會導致與伺服器之間的額外網路往返。  
  
> [!NOTE]  
>  在下列情況下，提供者不支援呼叫 **ICommandWithParameters::GetParameterInfo**：包含 FROM 子句的任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UPDATE 或 DELETE 陳述式、相依於包含參數之子查詢的任何 SQL 陳述式、在比較 (like) 或定量述詞的運算式中都包含參數標記的 SQL 陳述式，或是其中一個參數為函式參數的任何查詢。 在處理 SQL 陳述式批次時，提供者也不支援針對批次內第一個陳述式之後的陳述式中的參數標記呼叫 **ICommandWithParameters::GetParameterInfo**。 不允許在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令中使用註解 (/* \*/)。  
  
 OLE DB Driver for SQL Server 支援 SQL 陳述式命令中的輸入參數。 在程序呼叫命令中，OLE DB Driver for SQL Server 支援輸入、輸出及輸入/輸出參數。 在執行 (只有在沒有傳回任何資料列集時) 或應用程式已用盡所有傳回的資料列集時，輸出參數值就會傳回應用程式。 若要確保傳回的值有效，請使用 **IMultipleResults** 來強制資料列集取用。  
  
 您不需要在 DBPARAMBINDINFO 結構中指定預存程序參數的名稱。 您可以使用 NULL 當作 *pwszName* 成員的值，表示 OLE DB Driver for SQL Server 應該忽略參數名稱，而且僅使用 **ICommandWithParameters::SetParameterInfo** 之 *rgParamOrdinals* 成員中指定的序數。 如果命令文字同時包含已命名和未命名的參數，您就必須在任何已命名的參數前面指定所有未命名的參數。  
  
 如果指定預存程序參數的名稱，OLE DB Driver for SQL Server 就會檢查名稱，以便確保它是否有效。 當 OLE DB Driver for SQL Server 從取用者接收到錯誤的參數名稱時，就會傳回錯誤。  
  
> [!NOTE]  
>  為了公開 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 和使用者定義型別 (UDT) 的支援，OLE DB Driver for SQL Server 會實作新的 [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) 介面。  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
