---
title: "錯誤訊息 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6223cba-2dec-4b8a-bc10-e2ef6a821fe0
caps.latest.revision: "9"
ms.openlocfilehash: 7c7d453bc2ac68db724734d7db7cf58e35611ba8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="error-messages"></a>錯誤訊息
SQL Server PDW 錯誤訊息會報告錯誤和問題發生的 SQL Server PDW 元件，也可以包含透過 SQL Server PDW 的 SQL Server 錯誤。 這些錯誤訊息會使用一致的語法來顯示資訊。 了解此語法可讓您識別及更正 SQL Server PDW 上的問題。  
  
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
  
## <a name="see-also"></a>請參閱＜  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[了解管理主控台警示](understanding-admin-console-alerts.md)  
  
