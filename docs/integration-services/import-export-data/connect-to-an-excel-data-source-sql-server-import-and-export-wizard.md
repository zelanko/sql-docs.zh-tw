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
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d744e84aa2b4ae0462a5d5a1e4453a9e86abb890
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

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
> 您可能必須下載並安裝其他檔案，才能連接到您選取的 Excel 版本。 請參閱[取得您需要連接到 Excel 檔案](#officeDownloads)在此頁面上，如需詳細資訊。

如果指定了版本時，您會有問題，請嘗試指定不同的版本，即使較早的版本。 例如，您可能無法安裝 Office 2016 的資料提供者，因為您有 Microsoft Office 365 訂閱。 您只可以與 Microsoft Office 的桌面版本安裝 Excel 2016 和存取 2016年的資料提供者。 在此情況下，您可以指定 Excel 2013，而不是 Excel 2016。 兩個版本的提供者的功能相同。 Office 2016 的執行階段的這項限制中有提及[此部落格文章](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/)。

**第一個資料列有資料行名稱**  
指出第一個資料列是否包含資料行名稱。
-   如果資料不包含資料行名稱，但您啟用這個選項，精靈會將來源資料的第一列視為資料行名稱。
-   如果資料包含資料行名稱，但停用此選項，精靈會將資料行名稱的資料列視為資料的第一個資料列。

如果您指定的資料不會有資料行名稱，精靈會使用 F1、 F2 等等，做為資料行標題。

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>我沒看到 Excel 中的資料來源清單
如果您沒有看到 Excel 資料來源的清單中，您會執行 64 位元精靈嗎？ Excel 和 Access 的提供者是一般的 32 位元和 64 位元精靈 中看不到。 請改為執行 32 位元精靈。

## <a name="officeDownloads"></a>取得您需要連接到 Excel 檔案  
您可能要下載 Microsoft Office 的資料來源，包括 Excel 和 Access，如果它們尚未安裝連接元件。

新版的元件可以開啟舊版程式所建立的檔案。 在某些情況下，新版的元件也可以開啟舊版程式所建立的檔案。 例如，如果您無法安裝 Office 2016 元件，改用 Office 2013 元件。 兩個版本的提供者的功能相同。 Office 2016 的執行階段的這項限制中有提及[此部落格文章](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/)。

如果電腦有 32 位元版本的 Office-這是正常的狀況下，即使在 64 位元的電腦-您必須安裝 32 位元版本的元件。 您也必須確定您執行 32 位元精靈時，或執行 SQL Server Integration Services 封裝，精靈會建立在 32 位元模式。 
 
|Microsoft Office 版本|下載|  
|------------------------------|--------------|  
|2016|[Microsoft Access 2016 執行階段](https://www.microsoft.com/download/details.aspx?id=50040)|
|2013|[Microsoft Access 2013 執行階段](http://www.microsoft.com/download/details.aspx?id=39358)|
|2010|[Microsoft Access 2010 執行階段](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2007|[2007 Office System 驅動程式：資料連接元件](https://www.microsoft.com/download/details.aspx?id=23734)|  

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


