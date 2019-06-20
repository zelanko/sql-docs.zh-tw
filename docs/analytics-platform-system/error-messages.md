---
title: 錯誤訊息-Parallel Data Warehouse |Microsoft Docs
description: Parallel Data Warehouse (PDW) 錯誤訊息會報告錯誤和問題遇到的 PDW 元件，而且也可以包含 SQL Server PDW 透過顯示的錯誤。 這些錯誤訊息會使用一致的語法，來顯示資訊。 了解此語法可讓您識別並解決問題。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3ffc7a097845f4652f56d82c572ecfab868d33f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042594"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>平行處理資料倉儲中的錯誤訊息

Parallel Data Warehouse (PDW) 錯誤訊息會報告錯誤和問題遇到的 PDW 元件，而且也可以包含 SQL Server PDW 透過顯示的錯誤。 這些錯誤訊息會使用一致的語法，來顯示資訊。 了解此語法，可讓您找出並修正 SQL Server PDW 上的問題。  
  
## <a name="Basics"></a>錯誤訊息的基本概念  
會傳回的錯誤訊息會遵循相同的語法。  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
以下是可能的值，每個欄位：  
  
|欄位|描述|範例|  
|---------|---------------|-----------|  
|*Error_Indicator*|「 錯誤 」 這個字或其他文字警示使用者的問題。|error|  
|*SQL_State_Code*|SQL 狀態碼，根據 ODBC 規格。 驅動程式在任何時候，它會將訊息傳回至應用程式時，都會產生適當的 SQL 狀態程式碼。 "Microsoft"的文字表示錯誤的來源。|42000|  
|*Driver_Details*|驅動程式相關詳細資訊，例如使用驅動程式的類型。|ODBC SQL Server 2008 R2 Parallel Data Warehouse 驅動程式|  
|*QueryID*|查詢的唯一識別項。 使用此值來尋找與處理之查詢相關的其他資訊。 例如，查詢執行詳細資料可在管理主控台中使用查詢識別碼。 如需詳細資訊，請參閱 <<c0> [ 使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />如果 QueryID 不適用，「 內部 」 的文字會傳回給使用者。|QID2377|  
|*Message_String*|人類看得懂的錯誤或問題描述。 當傳回 SQL Server 錯誤，這會是 SQL Server 訊息文字。|只有相等指派可以出現在 UPDATE 陳述式的 set 清單中。|  
  
這些範例值會顯示給使用者，就像這樣：  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[了解系統管理員主控台的警示](understanding-admin-console-alerts.md)  
  
