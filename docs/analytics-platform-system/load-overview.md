---
title: 載入
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: 您可以載入或使用 Integration Services，bcp 公用程式、 dwloader 或 SQL INSERT 陳述式插入資料至 SQL Server Parallel Data Warehouse (PDW)。
ms.date: 10/20/2016
ms.topic: article
ms.assetid: c7292108-4a48-409e-b0f4-e4ba84dce26f
caps.latest.revision: 22
ms.openlocfilehash: 77bb7e3ba6a3377fe63decf06a872872eaa4ee61
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="load-sql-server-pdw"></a>載入 (SQL Server PDW)
您可以載入或插入資料至 SQL Server Parallel Data Warehouse (PDW) 使用 Integration Services [bcp 公用程式](../tools/bcp-utility.md)， **dwloader**命令列載入器或 SQL INSERT 陳述式。  

## <a name="loading-environment"></a>載入的環境  
若要載入資料，您需要一或多個載入伺服器。 您可以使用您自己現有的 ETL 或其他伺服器，或者，您可以購買新的伺服器。 如需詳細資訊，請參閱[取得和設定載入伺服器](acquire-and-configure-loading-server.md)。 這些指示包含[載入伺服器容量規劃工作表](loading-server-capacity-planning-worksheet.md)可協助您規劃載入正確的方案。  
  
## <a name="load-with-dwloader"></a>載入具有 dwloader  
使用[dwloader 命令列載入器](dwloader.md)是將資料載入至 PDW 最快的方法。  
  
![載入處理序](media/loading-process.png "載入程序")  
  
dwloader 載入直接用於運算節點的資料，而不傳遞控制節點的資料。 若要載入資料，dwloader 第一次會與通訊以取得運算節點的連絡資訊的控制節點。 dwloader 設定與每個計算節點的通訊通道，，然後在循環配置資源方式的計算節點傳送 256 KB 的資料區塊。  
  
每個計算節點上，資料移動服務 (DMS) 會接收和處理的資料區塊。 處理資料，包括將每個資料列轉換成 SQL Server 原生格式，並計算發佈雜湊，來判斷每個資料列所屬的計算節點。  
  
在處理資料列之後, DMS 會使用隨機移動傳送每個資料列的正確計算節點和 SQL Server 執行個體。 當 SQL Server 收到的資料列，則批次根據它們**– b** batch size 參數中 dwloader，所設定，然後再大量載入的批次。  

## <a name="load-with-prepared-statements"></a>載入與準備的陳述式

您可以使用已備妥的陳述式將資料載入至分散式和複寫的資料表。 當輸入的資料不符合目標資料類型時，則會執行隱含轉換。 PDW 備妥陳述式所支援的隱含轉換是 SQL Server 所支援轉換的子集。 也就是支援的轉換子集，但支援的轉換符合 SQL Server 的隱含轉換。 不論是否要載入目標資料表定義為分散式或複寫資料表時，隱含的轉換會套用 （如有需要） 存在於目標資料表中的所有資料行。 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>相關工作  
  
|工作|Description|  
|--------|---------------|  
|建立暫存資料庫。|[建立暫存資料庫](staging-database.md)|  
|載入 with Integration Services。|[使用 Integration Services 載入](load-with-ssis.md)|  
|了解 dwloader 的型別轉換。|[dwloader 的資料類型轉換規則](dwloader-data-type-conversion-rules.md)|  
|載入資料有 dwloader。|[dwloader 命令列載入器](dwloader.md)|  
|了解針對插入的型別轉換。|[使用 INSERT 載入資料](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
