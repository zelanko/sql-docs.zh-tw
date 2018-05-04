---
title: 命令參數 |Microsoft 文件
description: 命令參數
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- parameters [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, parameters
- OLE DB Driver for SQL Server, commands
- parameters [OLE DB Driver for SQL Server], OLE DB
- commands [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: f32f4adf2bc4d969154741edc447d942e7b62d37
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="command-parameters"></a>命令參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在命令文字中，參數會以問號字元來標示。 例如，下列 SQL 陳述式是針對單一輸入參數標示：  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 若要降低網路流量來改善效能，SQL Server OLE DB 驅動程式不會自動衍生參數資訊除非**icommandwithparameters:: Getparameterinfo**或**m::準備**執行命令之前呼叫。 這表示 SQL Server OLE DB 驅動程式不會自動：  
  
-   驗證具有指定的資料類型的正確性**icommandwithparameters:: Setparameterinfo**。  
  
-   從存取子繫結資訊中指定的 DBTYPE 對應至參數的正確 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。  
  
 如果應用程式指定了與參數之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型不相容的資料類型，它們將在使用其中一種方法時收到可能的錯誤或遺失有效位數。  
  
 若要確保不會發生這種情況，應用程式應該：  
  
-   請確認*pwszDataSourceType*符合[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別參數，如果硬式編碼**icommandwithparameters:: Setparameterinfo**。  
  
-   確定繫結至參數的 DBTYPE 值與參數的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型具有相同的類型 (如果寫入存取子程式碼的話)。  
  
-   程式碼應用程式呼叫**icommandwithparameters:: Getparameterinfo** ，讓提供者可以取得[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別參數的動態。 請注意，這可能會導致與伺服器之間的額外網路往返。  
  
> [!NOTE]  
>  提供者不支援呼叫**icommandwithparameters:: Getparameterinfo**任何[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]UPDATE 或 DELETE 陳述式包含 FROM 子句; 針對任何 SQL 陳述式，根據子查詢包含參數。SQL 陳述式中包含參數標記的比較，這兩個運算式，或定量述詞。或其中一個參數是函式的參數的查詢。 在處理 SQL 陳述式的批次時，提供者也不支援呼叫**icommandwithparameters:: Getparameterinfo**批次中的第一個陳述式之後的陳述式中的參數標記。 註解 (/ * \*/) 中不允許[!INCLUDE[tsql](../../../includes/tsql-md.md)]命令。  
  
 SQL Server OLE DB 驅動程式支援 SQL 陳述式命令中的輸入的參數。 在程序呼叫命令中，SQL Server OLE DB 驅動程式支援輸入、 輸出和輸入/輸出參數。 在執行 (只有在沒有傳回任何資料列集時) 或應用程式已用盡所有傳回的資料列集時，輸出參數值就會傳回應用程式。 若要確保傳回的值有效，使用**IMultipleResults**強制資料列集取用。  
  
 您不需要在 DBPARAMBINDINFO 結構中指定預存程序參數的名稱。 使用 NULL 值的*pwszName*成員表示 SQL Server OLE DB 驅動程式，應該忽略參數名稱，使用中指定的序數*可以*的成員**Icommandwithparameters:: Setparameterinfo**。 如果命令文字同時包含已命名和未命名的參數，您就必須在任何已命名的參數前面指定所有未命名的參數。  
  
 如果指定了預存程序參數的名稱，則 SQL Server OLE DB 驅動程式會檢查名稱，以便確保它有效。 從取用者收到錯誤的參數名稱時，SQL Server OLE DB 驅動程式會傳回錯誤。  
  
> [!NOTE]  
>  若要公開支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]XML 和使用者定義型別 (UDT)，SQL Server OLE DB 驅動程式會實作新[ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)介面。  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
