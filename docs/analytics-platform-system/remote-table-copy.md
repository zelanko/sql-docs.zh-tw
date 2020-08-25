---
title: 遠端資料表複本
description: 使用 Analytics Platform System 平行處理資料倉儲中的遠端資料表複製。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ecbbdced731e940de46dbde4a65adc486f602c2f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400484"
---
# <a name="remote-table-copy"></a>遠端資料表複製
描述如何使用遠端資料表複製功能，將資料表從 SQL Server PDW 資料庫複製到遠端 (非設備) SMP SQL Server 資料庫。 使用遠端資料表複製來啟用 SQL Server PDW 的中樞和輪輻案例。  
  
## <a name="understand-remote-table-copy-for-sql-server-pdw"></a><a name="BasicsPDE"></a>瞭解 SQL Server PDW 的遠端資料表複本  
遠端資料表複製是 SQL Server PDW 的功能，可將 SQL SELECT 語句的結果複製到 SMP 資料庫中的資料表，藉此啟用中樞和輪輻案例。 使用 [CREATE REMOTE table AS SELECT 語句來](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) 起始遠端資料表複本。  
  
## <a name="requirements-for-using-remote-table-copy"></a><a name="BasicsPrerequisites"></a>使用遠端資料表複製的需求  
當符合下列條件時，您可以使用遠端資料表複製將資料表從 SQL Server PDW 複製到 SQL Server 資料庫：  
  
-   目的地資料庫必須是在 Microsoft Windows®系統上執行的 Microsoft® SQL Server®的實例，該系統可連接至 SQL Server PDW 設備，但不在設備內的伺服器上。 遠端 SQL Server 可以使用未受網路或乙太網路的網路連線到 SQL Server PDW。  
  
-   您必須使用單一有效的 SQL Server PDW [SELECT](../t-sql/queries/select-transact-sql.md) 語句來選取要複製的資料。  
  
-   目的地伺服器必須是非應用裝置伺服器。 您可以使用本主題中的指示，將資料直接從某個設備複製到另一個應用裝置。  
  
-   目的地伺服器必須可供設備的所有節點上的所有節點存取。  
  
## <a name="configure-remote-table-copy"></a><a name="ConfigureRemote"></a>設定遠端資料表複製  
若要使用遠端資料表複製，您必須購買和設定 Windows server、在 Windows server 上設定 SQL Server，以及設定 SQL Server PDW。 您可以使用下列連結來執行這三個設定步驟。  
  
1.  [設定外部 Windows 系統以使用「不使用」來接收遠端資料表複本](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [設定外部 SMP SQL Server 接收遠端資料表複本](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [設定遠端資料表複本的 SQL Server PDW](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="perform-a-remote-table-copy"></a><a name="PerformRemote"></a>執行遠端資料表複製  
若要執行遠端資料表複製，請使用 [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL 語句。 範例包含在 CREATE REMOTE TABLE 主題中。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
