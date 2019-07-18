---
title: 將資料載入至 Parallel Data Warehouse |Microsoft Docs
description: 您可以載入或使用 Integration Services、 bcp 公用程式、 dwloader 或 SQL INSERT 陳述式插入資料至 SQL Server Parallel Data Warehouse (PDW)。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b046839b7c4932b43230d28cc106db1e2ea5d5a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960696"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>將資料載入至平行處理資料倉儲
您可以載入或插入資料至 SQL Server Parallel Data Warehouse (PDW) 使用 Integration Services [bcp 公用程式](../tools/bcp-utility.md)， **dwloader**命令列載入器或 SQL INSERT 陳述式。  

## <a name="loading-environment"></a>正在載入環境  
若要載入資料，您需要一或多個載入伺服器。 您可以使用您自己現有的 ETL 或其他伺服器，或您可以購買新的伺服器。 如需詳細資訊，請參閱 <<c0> [ 取得並設定載入伺服器](acquire-and-configure-loading-server.md)。 這些指示包含[載入伺服器容量規劃工作表](loading-server-capacity-planning-worksheet.md)可協助您規劃載入適合的解決方案。  
  
## <a name="load-with-dwloader"></a>使用 dwloader 載入資料  
使用[dwloader 命令列載入器](dwloader.md)最快的方法，將資料載入 PDW。  
  
![載入程序](media/loading-process.png "載入程序")  
  
dwloader 載入直接至計算節點的資料，而不傳遞控制節點的資料。 若要載入資料，dwloader 第一次會與通訊以取得連絡資訊的計算節點的 [控制] 節點。 dwloader 設定與每個計算節點的通訊通道，並以循環配置資源的方式，然後將 256 KB 區塊計費的資料傳送至計算節點。  
  
每個計算節點上，資料移動服務 (DMS) 會接收並處理的資料區塊。 處理資料，包括將每個資料列轉換成 SQL Server 原生格式，並計算散發雜湊來判斷每個資料列所屬的計算節點。  
  
之後處理這些資料列，DMS 會傳送至正確的計算節點和 SQL Server 執行個體的每個資料列，使用 「 隨機 」 移動。 SQL Server 收到的資料列，它會批次處理它們根據 **-b**集 dwloader，批次大小參數，然後大量載入批次。  

## <a name="load-with-prepared-statements"></a>載入已備妥的陳述式

您可以使用已備妥的陳述式將資料載入至分散式且複寫的資料表。 當輸入的資料不符合目標資料類型時，會執行隱含轉換。 PDW 備妥陳述式所支援的隱含轉換是由 SQL Server 支援的轉換子集。 也就是支援的轉換子集，但支援的轉換符合 SQL Server 的隱含轉換。 不論是否要載入目標資料表定義為分散式或複寫資料表時，隱含轉換會套用 （如有需要） 至目標資料表中的所有資料行。 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>相關工作  
  
|工作|描述|  
|--------|---------------|  
|建立暫存資料庫。|[建立暫存資料庫](staging-database.md)|  
|使用 Integration Services 載入資料。|[使用 Integration Services 載入](load-with-ssis.md)|  
|了解 dwloader 的型別轉換。|[dwloader 的資料類型轉換規則](dwloader-data-type-conversion-rules.md)|  
|載入 dwloader 的資料。|[dwloader 命令列載入器](dwloader.md)|  
|了解插入的型別轉換。|[使用 INSERT 載入資料](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
