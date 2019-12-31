---
title: 遠端資料表複本
description: 流量分析平臺系統平行處理資料倉儲中的遠端資料表複本。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ecbbdced731e940de46dbde4a65adc486f602c2f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400484"
---
# <a name="remote-table-copy"></a>遠端資料表複本
描述如何使用遠端資料表複製功能，將資料表從 SQL Server PDW 資料庫複製到遠端（非應用裝置） SMP SQL Server 資料庫。 使用遠端資料表複本來啟用 SQL Server PDW 的中樞和輪輻案例。  
  
## <a name="BasicsPDE"></a>瞭解 SQL Server PDW 的遠端資料表複本  
遠端資料表複本是 SQL Server PDW 的一項功能，可將 SQL SELECT 語句的結果複製到 SMP 資料庫中的資料表，藉此啟用中樞和輪輻案例。 使用[CREATE REMOTE table AS SELECT 語句來](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md)起始遠端資料表複本。  
  
## <a name="BasicsPrerequisites"></a>使用遠端資料表複製的需求  
當符合下列條件時，您可以使用遠端資料表複本，將資料表從 SQL Server PDW 複製到 SQL Server 資料庫：  
  
-   目的地資料庫必須是在 Microsoft Windows®系統上執行的 Microsoft® SQL Server®實例，而該系統可以連接到 SQL Server PDW 設備，但不在設備內的伺服器上。 遠端 SQL Server 可以使用未經過的網路或透過 Ethernet 網路連接到 SQL Server PDW。  
  
-   要複製的資料必須使用單一有效的 SQL Server PDW [SELECT](../t-sql/queries/select-transact-sql.md)語句來選取。  
  
-   目的地伺服器必須是非應用裝置伺服器。 您無法使用本主題中的指示，將資料直接從一個應用裝置複製到另一個設備。  
  
-   目的地伺服器必須可供設備的不會的網路上的所有節點存取。  
  
## <a name="ConfigureRemote"></a>設定遠端資料表複本  
若要使用遠端資料表複製，您需要購買和設定 Windows server、在 Windows server 上設定 SQL Server，以及設定 SQL Server PDW。 使用下列連結來執行這三個設定步驟。  
  
1.  [設定外部 Windows 系統，以使用不限時間接收遠端資料表複本](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [設定外部 SMP SQL Server 以接收遠端資料表複本](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [設定遠端資料表複本的 SQL Server PDW](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>執行遠端資料表複製  
若要執行遠端資料表複本，請使用[CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL 語句。 建立遠端資料表主題中包含範例。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
