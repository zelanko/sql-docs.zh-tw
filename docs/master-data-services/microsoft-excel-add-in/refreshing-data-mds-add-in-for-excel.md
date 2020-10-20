---
description: 重新整理資料 (適用於 Excel 的 MDS 增益集)
title: 重新整理資料
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 58dbe99a-288d-4f1c-9cd5-704d6836c945
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e9fe89ec7abff9a3440b72bb00d4aaee86837ca4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257775"
---
# <a name="refreshing-data-mds-add-in-for-excel"></a>重新整理資料 (適用於 Excel 的 MDS 增益集)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，當您想要從 MDS 存放庫取得最新資訊，而不開啟新的工作表時，請重新整理資料。 您可以重新整理所有資料格或資料格的選取範圍。 當您已經插入含有自訂公式或不在 MDS 中管理之資料的資料行，而且想要加以保留時，這樣做可能很有用。  
  
## <a name="when-you-can-refresh-mds-managed-data"></a>何時能夠重新整理 MDS 管理的資料  
 如果使用中工作表已經包含 MDS 管理的資料，您就可以在使用中工作表中重新整理 MDS 管理的資料。 如果您已經變更屬性值或將成員加入至工作表，就必須先發行變更，然後才能重新整理。  
  
## <a name="refreshing-a-selection"></a>重新整理選取範圍  
 您可以選擇重新整理所有資料格或只重新整理選取的資料格。 選取的資料格必須是連續的。 如果選取一組連續的資料格，該集合中所有 MDS 管理的資料格都會更新，以顯示目前儲存在伺服器上的值。 未變更且 MDS 未管理的資料列與資料行無論如何都不受影響。  
  
## <a name="what-happens-when-you-refresh-mds-managed-data"></a>重新整理 MDS 管理的資料時會發生什麼狀況  
 當您在 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中重新整理資料時，工作表處理 MDS 管理之資料的方式，取決從您上次載入資料之後 MDS 存放庫變更了哪些內容而定。  
  
-   如果新的成員已經加入至儲存機制，它們就會加入至工作表的結尾並且以綠色反白顯示。  
  
-   如果儲存機制已刪除成員，系統就會從工作表中刪除它們。  
  
-   如果 MDS 儲存機制中的某個屬性值已變更，工作表中的值就會使用 MDS 儲存機制中的值來更新。 資料格色彩不會變更。  
  
> [!WARNING]
>  -   在使用中工作表中，如果非管理的資料存在 MDS 管理之資料下方的資料列中，系統可能會覆寫非管理的資料。 當您重新整理工作表，而且加入 MDS 管理之資料的新資料列 (與非管理的資料重疊) 時，就會發生這種狀況。  
> -   當您重新整理時，系統會刪除 MDS 管理之資料格的註解。  
  
## <a name="how-to-refresh-mds-managed-data"></a>如何重新整理 MDS 管理的資料  
 在功能區的 [連接和載入]**** 群組中，[重新整理]**** 按鈕有兩個選項，分別是 [全部重新整理]**** 和 [重新整理選取項目]****。 功能區按鈕的預設動作是 [全部重新整理]****。 若要使用來自伺服器的值重新整理整份工作表，按一下 [重新整理]**** 按鈕，或選擇 [全部重新整理]**** 選項。 若僅要重新整理工作表中的部分資料格，請選取資料格 (必須是一個連續的選取範圍)，然後選擇 [重新整理選取項目]**** 選項。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的連接。|[連接到 MDS 儲存機制 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|將 MDS 資料載入 Excel 中。|[將資料從 Master Data Services 匯出至 Excel](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [連接 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [概觀：將資料匯出至 Excel &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [適用於 Microsoft Excel 的 Master Data Services 增益集](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  
