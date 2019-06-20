---
title: 遠端資料表複製-Parallel Data Warehouse |Microsoft Docs
description: Analytics Platform System 平行處理資料倉儲中使用遠端資料表複本。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5ed517a471368e4192ad7393a92274424d37f975
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678558"
---
# <a name="remote-table-copy"></a>遠端資料表複製
描述如何將資料表從 SQL Server PDW 資料庫複製到遠端的 （非應用裝置） SMP SQL Server 資料庫時，用於遠端資料表複製功能。 使用遠端資料表複製到可讓中樞和支點案例適用於 SQL Server PDW。  
  
## <a name="BasicsPDE"></a>了解適用於 SQL Server PDW 的遠端資料表複製  
遠端資料表複本是一項功能的 SQL Server PDW，也能將 SQL SELECT 陳述式的結果複製到 SMP 資料庫的資料表中的中樞和輪輻的案例。 使用起始遠端資料表複本[建立 REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md)陳述式。  
  
## <a name="BasicsPrerequisites"></a>使用遠端資料表複製的需求  
符合這些條件時，您可以使用從 SQL Server PDW 」 至 SQL Server 資料庫中的遠端資料表複製到複製資料表：  
  
-   目的地資料庫必須可以連線到 SQL Server PDW 應用裝置，但不在應用裝置內的伺服器上的 Microsoft Windows® 系統執行的 Microsoft® SQL Server® 的執行個體。 遠端 SQL Server 可以連接到 SQL Server PDW 使用 InfiniBand 網路或透過乙太網路。  
  
-   要複製的資料必須是可使用單一的有效 SQL Server PDW[選取](../t-sql/queries/select-transact-sql.md)陳述式。  
  
-   目的地伺服器必須是非應用裝置伺服器。 資料無法直接從一個應用裝置複製到另一個使用指示在本主題中。  
  
-   目的地伺服器必須能夠在設備的 Infiniband 網路上的所有節點。  
  
## <a name="ConfigureRemote"></a>設定遠端資料表複本  
若要使用的遠端資料表複本，您需要購買及設定 Windows 伺服器，在 Windows 伺服器上，設定 SQL Server 及設定 SQL Server PDW。 您可以使用下列連結來執行下列三個設定步驟。  
  
1.  [設定外部 Windows 系統，以接收遠端資料表複本使用 InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [設定外部 SMP SQL 伺服器以接收遠端資料表複本](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [設定用於遠端資料表複本的 SQL Server PDW](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>執行遠端資料表複製  
若要執行的遠端資料表複本，請使用[建立 REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL 陳述式。 範例包括隨附於 CREATE REMOTE TABLE 主題。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
