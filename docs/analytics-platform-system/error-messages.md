---
title: 錯誤訊息
description: 平行處理資料倉儲（PDW）錯誤訊息會報告 PDW 元件遇到的錯誤和問題，而且也可以包含透過 PDW 呈現的 SQL Server 錯誤。 這些錯誤訊息會使用一致的語法來呈現資訊。 瞭解此語法可讓您找出問題並加以修正。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2d89e80a89df53e85ef8d2bf53c369d9e4dc0d49
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401160"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>平行處理資料倉儲中的錯誤訊息

平行處理資料倉儲（PDW）錯誤訊息會報告 PDW 元件遇到的錯誤和問題，而且也可以包含透過 PDW 呈現的 SQL Server 錯誤。 這些錯誤訊息會使用一致的語法來呈現資訊。 瞭解此語法可讓您找出並修正 SQL Server PDW 上的問題。  
  
## <a name="error-message-basics"></a><a name="Basics"></a>錯誤訊息基本概念  
傳回的錯誤訊息會遵循相同的語法。  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
以下是每個欄位的可能值：  
  
|欄位|描述|範例|  
|---------|---------------|-----------|  
|*Error_Indicator*|"ERROR" 或其他文字一詞會警示使用者發生問題。|ERROR|  
|*SQL_State_Code*|SQL 狀態碼（根據 ODBC 規格）。 驅動程式會在每次將訊息傳回至應用程式時，產生適當的 SQL 狀態碼。 文字 "Microsoft" 表示錯誤的來源。|42000|  
|*Driver_Details*|與驅動程式相關的詳細資料，例如所使用的驅動程式類型。|ODBC SQL Server 2008 R2 平行處理資料倉儲驅動程式|  
|*QueryID*|查詢的唯一識別碼。 使用此值來尋找與處理查詢相關的其他資訊。 例如，您可以使用查詢識別碼，在管理主控台中找到查詢執行詳細資料。 如需詳細資訊，請參閱[使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />如果 QueryID 不適用，則會將 "Internal" 文字傳回給使用者。|QID2377|  
|*Message_String*|人類看得懂的錯誤或問題描述。 傳回 SQL Server 錯誤時，這就是 SQL Server 郵件內文。|UPDATE 語句的 set 清單中只能出現相等的指派。|  
  
這些範例值會呈現給使用者，如下所示：  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[瞭解管理主控台警示](understanding-admin-console-alerts.md)  
  
