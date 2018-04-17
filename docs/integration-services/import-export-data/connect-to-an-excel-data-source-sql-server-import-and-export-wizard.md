---
title: 連線至 Excel 資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 42af9f992c293f9872080a69cf6a7a4890ff205f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>連線至 Excel 資料來源 (SQL Server 匯入和匯出精靈)
本主題示範如何從 [SQL Server 匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面中連線至 **Microsoft Excel** 資料來源。

下列螢幕擷取畫面顯示 Microsoft Excel 活頁簿的連接範例。

![Excel 連接](../../integration-services/import-export-data/media/excel-connection.png) 

您可能必須下載並安裝其他檔案，才能連線至 Excel 檔案。 如需詳細資訊，請參閱[取得連線至 Excel 所需的檔案](../load-data-to-from-excel-with-ssis.md#get-the-files-you-need-to-connect-to-excel)。

> [!IMPORTANT]
> 如需連線至 Excel 檔案，以及對 Excel 檔案載入資料進出的限制與已知問題之詳細資訊，請參閱[利用 SQL Server Integration Services (SSIS) 對 Excel 載入資料進出](../load-data-to-from-excel-with-ssis.md)。

## <a name="options-to-specify"></a>要指定的選項

> [!NOTE]
> 不論 Excel 是您的來源還是目的地，此資料提供者的連線選項都會相同。 也就是，您在精靈的 [選擇資料來源] 和 [選擇目的地] 頁面上看到的選項會相同。

**Excel 檔案路徑**  
 指定 Excel 檔案的路徑和檔案名稱。 例如：
-   本機電腦上的檔案為 **C:\\MyData.xlsx**。
-   網路共用上的檔案為 **\\\\Sales\\Database\\Northwind.xlsx**。

或按一下 [瀏覽]。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出試算表。  

> [!NOTE]
> 精靈無法開啟受密碼保護的 Excel 檔案。

 **Excel 版本**  
請選取來源或目的地活頁簿所使用的 Excel 版本。

**第一個資料列有資料行名稱**  
指出資料的第一個資料列是否包含資料行名稱。
-   如果資料不包含資料行名稱，但您啟用了此選項，則精靈會將來源資料的第一列視為資料行名稱。
-   如果資料包含資料行名稱，但您停用了此選項，則精靈會將資料行名稱的資料列視為資料的第一列。

如果您指定資料沒有資料行名稱，則精靈會在內部使用 F1、F2 等等作為資料行標題。

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>我在資料來源清單中看不到 Excel
如果您在資料來源清單中看不到 Excel，您是否執行 64 位元精靈？ Excel 和 Access 的提供者一般是 32 位元，而且在 64 位元精靈中看不到。 請改執行 32 位元精靈。

> [!NOTE]
> 若要使用 64 位元版本的 [SQL Server 匯入和匯出精靈]，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，而且只會安裝 32 位元檔案 (包含 32 位元版本的精靈)。

## <a name="see-also"></a>另請參閱
[利用 SQL Server Integration Services (SSIS) 對 Excel 載入資料進出](../load-data-to-from-excel-with-ssis.md)  
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

