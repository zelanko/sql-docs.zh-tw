---
title: 載入資料
description: 您可以使用 Integration Services、bcp 公用程式、dwloader 或 SQL INSERT 語句，將資料載入或插入 SQL Server 平行資料倉儲 (PDW) 。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd161820fd53d45642848697bce9589a98dec4ca
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74401042"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>將資料載入平行資料倉儲
您可以使用 Integration Services、 [Bcp 公用程式](../tools/bcp-utility.md)、 **Dwloader** 命令列載入器或 SQL insert 語句，將資料載入或插入 SQL Server 平行資料倉儲 (PDW) 。  

## <a name="loading-environment"></a>載入環境  
若要載入資料，您需要一或多個載入伺服器。 您可以使用自己現有的 ETL 或其他伺服器，也可以購買新的伺服器。 如需詳細資訊，請參閱 [取得和設定載入伺服器](acquire-and-configure-loading-server.md)。 這些指示包含 [載入伺服器容量規劃工作表](loading-server-capacity-planning-worksheet.md) ，可協助您規劃適合載入的解決方案。  
  
## <a name="load-with-dwloader"></a>使用 dwloader 載入  
使用 [Dwloader 命令列載入](dwloader.md) 器是將資料載入 PDW 最快的方式。  
  
![正在載入進程](media/loading-process.png "載入處理序")  
  
dwloader 會將資料直接載入至計算節點，而不需透過控制節點傳遞資料。 若要載入資料，dwloader 會先與控制項節點進行通訊，以取得計算節點的連絡人資訊。 dwloader 會設定每個計算節點的通道，然後以迴圈配置資源的方式，將256KB 區塊的資料傳送至計算節點。  
  
在每個計算節點上，資料移動服務 (DMS) 接收和處理資料區塊。 處理資料包括將每一個資料列轉換成 SQL Server 原生格式，以及計算分佈雜湊以判斷每個資料列所屬的計算節點。  
  
在處理資料列之後，DMS 會使用隨機移動，將每個資料列傳送到正確的計算節點和 SQL Server 的實例。 當 SQL Server 接收資料列時，它會根據 dwloader 中設定的 **-b** 批次大小參數進行批次處理，然後大量載入批次。  

## <a name="load-with-prepared-statements"></a>具有備妥語句的載入

您可以使用已備妥的語句，將資料載入分散式和複寫資料表中。 當輸入資料與目標資料類型不相符時，就會執行隱含轉換。 PDW 備妥語句所支援的隱含轉換是 SQL Server 所支援的轉換子集。 也就是說，只支援轉換的子集，但支援的轉換符合 SQL Server 隱含轉換。 無論要載入的目標資料表是定義為分散式或複寫資料表，如果需要) 到存在於目標資料表中的所有資料行，則隱含轉換會套用 (。 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>相關工作  
  
|Task|描述|  
|--------|---------------|  
|建立臨時資料庫。|[建立臨時資料庫](staging-database.md)|  
|使用 Integration Services 載入。|[使用 Integration Services 載入](load-with-ssis.md)|  
|瞭解 dwloader 的類型轉換。|[dwloader 的資料類型轉換規則](dwloader-data-type-conversion-rules.md)|  
|使用 dwloader 載入資料。|[dwloader 命令列載入器](dwloader.md)|  
|瞭解 INSERT 的型別轉換。|[使用 INSERT 載入資料](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
