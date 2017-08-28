---
title: "連接至 Excel 資料來源 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: b4411fdd2337d93f15b149febf845fb7b0762c40
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>連接至 Excel 資料來源 （SQL Server 匯入和匯出精靈）
本主題說明如何連接到**Microsoft Excel**資料來源從**選擇資料來源**或**選擇目的地**SQL Server 匯入和匯出精靈 頁面。

下列螢幕擷取畫面顯示 Microsoft Excel 活頁簿的連接範例。

![Excel 連接](../../integration-services/import-export-data/media/excel-connection.png) 

## <a name="options-to-specify"></a>若要指定的選項

> [!NOTE]
> Excel 是您的來源或目的地連接選項，此資料提供者都是相同的。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

**Excel 檔案路徑**  
 指定 Excel 檔案的路徑和檔案名稱。 例如：
-   在本機電腦上的檔案**c:\\MyData.xlsx**。
-   網路共用上的檔案 **\\\\銷售\\資料庫\\Northwind.xlsx**。

或按一下 [瀏覽]。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出試算表。  

> [!NOTE]
> 精靈無法開啟受密碼保護的 Excel 檔案。

 **Excel 版本**  
選取來源活頁簿所使用的 Excel 版本。

> [!IMPORTANT]
> 您可能要下載並安裝其他要連接到 Excel 檔案的檔案。 請參閱[取得您需要連接到 Excel 檔案](#officeDownloads)在此頁面上，如需詳細資訊。

**第一個資料列有資料行名稱**  
指出第一個資料列是否包含資料行名稱。
-   如果資料不包含資料行名稱，但您啟用這個選項，精靈會將來源資料的第一列視為資料行名稱。
-   如果資料包含資料行名稱，但停用此選項，精靈會將資料行名稱的資料列視為資料的第一個資料列。

如果您指定的資料不會有資料行名稱，精靈會使用 F1、 F2 等等，做為資料行標題。

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>我沒看到 Excel 中的資料來源清單
如果您沒有看到 Excel 資料來源的清單中，您會執行 64 位元精靈嗎？ Excel 和 Access 的提供者是一般的 32 位元和 64 位元精靈 中看不到。 請改為執行 32 位元精靈。

> [!NOTE]
> 若要使用 64 位元版本的 SQL Server 匯入和匯出精靈，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，並只安裝 32 位元檔案，包括 32 位元版本的精靈。

## <a name="officeDownloads"></a>取得您需要連接到 Excel 檔案  
您可能要下載 Microsoft Office 的資料來源，包括 Excel 和 Access，如果它們尚未安裝連接元件。 下載最新版的 Excel 和 Access 檔案的連線元件： [Microsoft Access 資料庫引擎 2016年可轉散發套件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
最新版本的元件可以開啟以舊版 Excel 建立的檔案。

如果電腦有 32 位元版本的 Office，則必須安裝 32 位元版本的元件，而且您也必須確定您在 32 位元模式執行封裝。

如果您有 Office 365 訂閱，請確定您在 Access 資料庫引擎 2016年可轉散發套件並不使用 Microsoft Access 2016 執行階段時下載。 當您執行安裝程式時，您可能會看到錯誤訊息，您無法安裝下載的並存 Office 按一下來執行元件。 略過此錯誤訊息，以執行安裝以無訊息模式開啟命令提示字元視窗並執行。下載的 EXE 檔案`/quiet`切換。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


