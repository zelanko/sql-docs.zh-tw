---
title: "連線至 Excel 資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2aeb225037970b8a77169db18c204ecf6d4c19d6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>連線至 Excel 資料來源 (SQL Server 匯入和匯出精靈)
本主題示範如何從 [SQL Server 匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面中連線至 **Microsoft Excel** 資料來源。

下列螢幕擷取畫面顯示 Microsoft Excel 活頁簿的連接範例。

![Excel 連接](../../integration-services/import-export-data/media/excel-connection.png) 

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
選取來源活頁簿所使用的 Excel 版本。

> [!IMPORTANT]
> 您可能必須下載並安裝其他檔案，才能連線至 Excel 檔案。 如需詳細資訊，請參閱此頁面上的[取得連線至 Excel 所需的檔案](#officeDownloads)。

**第一個資料列有資料行名稱**  
指出資料的第一個資料列是否包含資料行名稱。
-   如果資料不包含資料行名稱，但您啟用了此選項，則精靈會將來源資料的第一列視為資料行名稱。
-   如果資料包含資料行名稱，但您停用了此選項，則精靈會將資料行名稱的資料列視為資料的第一列。

如果您指定資料沒有資料行名稱，則精靈會在內部使用 F1、F2 等等作為資料行標題。

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>我在資料來源清單中看不到 Excel
如果您在資料來源清單中看不到 Excel，您是否執行 64 位元精靈？ Excel 和 Access 的提供者一般是 32 位元，而且在 64 位元精靈中看不到。 請改執行 32 位元精靈。

> [!NOTE]
> 若要使用 64 位元版本的 [SQL Server 匯入和匯出精靈]，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，而且只會安裝 32 位元檔案 (包含 32 位元版本的精靈)。

## <a name="officeDownloads"></a>取得連線至 Excel 所需的檔案  
您可能必須下載尚未安裝的 Microsoft Office 資料來源 (包含 Excel 和 Access) 的連線元件。 在這裡下載 Excel 和 Access 檔案的連線元件最新版本：[Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920) (Microsoft Access Database Engine 2016 可轉散發套件)。
  
最新版的元件可以開啟舊版 Excel 所建立的檔案。

如果電腦有 32 位元版本的 Office，則必須安裝 32 位元版本的元件，而且您也必須確定以 32 位元模式執行套件。

如果您有 Office 365 訂用帳戶，請確定下載 Access Database Engine 2016 可轉散發套件，而非 Microsoft Access 2016 Runtime。 當您執行安裝程式時，可能會看到錯誤訊息，指出您無法使用 Office 隨選即用元件並存安裝下載。 若要略過此錯誤訊息，請開啟 [命令提示字元] 視窗並執行使用 `/quiet` 參數所下載的 .EXE 檔案，以無訊息模式執行安裝。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

