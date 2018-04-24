---
title: 錯誤訊息-Parallel Data Warehouse |Microsoft 文件
description: Parallel Data Warehouse (PDW) 錯誤訊息會報告錯誤和問題發生的 PDW 元件，也可以包含 SQL Server PDW 中顯示的錯誤。 這些錯誤訊息會使用一致的語法來顯示資訊。 了解此語法可讓您識別並修正問題。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 33bdf11388ae52959d264e2df091e9c9669b159b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
---
# <a name="error-messages-in-parallel-data-warehouse"></a>平行處理資料倉儲中的錯誤訊息

Parallel Data Warehouse (PDW) 錯誤訊息會報告錯誤和問題發生的 PDW 元件，也可以包含 SQL Server PDW 中顯示的錯誤。 這些錯誤訊息會使用一致的語法來顯示資訊。 了解此語法可讓您識別及更正 SQL Server PDW 上的問題。  
  
## <a name="Basics"></a>錯誤訊息的基本概念  
傳回的錯誤訊息會遵循相同的語法。  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
每個欄位的可能值如下：  
  
|欄位|Description|範例|  
|---------|---------------|-----------|  
|*Error_Indicator*|Word"ERROR"或其他文字警示使用者的問題。|ERROR|  
|*SQL_State_Code*|SQL 狀態碼，根據 ODBC 規格。 驅動程式會產生適當的 SQL 狀態碼的隨時它傳回至應用程式的訊息。 "Microsoft"的文字表示錯誤的來源。|42000|  
|*Driver_Details*|驅動程式相關詳細資料，例如使用驅動程式的類型。|ODBC SQL Server 2008 R2 Parallel Data Warehouse 驅動程式|  
|*QueryID*|查詢的唯一識別項。 使用此值來尋找與處理之查詢相關的其他資訊。 例如，查詢執行詳細資料可以找到管理主控台中使用的查詢識別碼。 如需詳細資訊，請參閱[使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />如果 QueryID 不適用，「 內部 」 的文字會傳回給使用者。|QID2377|  
|*Message_String*|人類看得懂的錯誤或問題描述。 在傳回 SQL Server 錯誤，這是 SQL Server 訊息文字。|只有相等指派可以出現在 UPDATE 陳述式的 set 清單中。|  
  
這些範例值會呈現給使用者，就像這樣：  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[了解管理主控台警示](understanding-admin-console-alerts.md)  
  
