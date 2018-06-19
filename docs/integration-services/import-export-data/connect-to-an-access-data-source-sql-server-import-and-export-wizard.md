---
title: 連線至 Access 資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 22356a0a1f15daebb47bfeb1beecfeae87a8bcc1
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403520"
---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>連線至 Access 資料來源 (SQL Server 匯入和匯出精靈)
本主題示範如何從 [SQL Server 匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面中連線至 **Microsoft Access** 資料來源。

下列螢幕擷取畫面顯示 Microsoft Access 資料庫的連接範例。 在此範例中，您不需要輸入使用者名稱和密碼，因為目標資料庫不會使用工作群組資訊檔案。

![連線至 Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>要指定的選項

> [!NOTE]
> 不論 Access 是您的來源還是目的地，此資料提供者的連線選項都會相同。 也就是，您在精靈的 [選擇資料來源] 和 [選擇目的地] 頁面上看到的選項會相同。

**資料來源**  
資料提供者清單可能包含數個 Microsoft Access 項目。 選取最新已安裝版本，或對應至已建立資料庫檔案之 Access 版本的版本。

|資料來源|Office 版本|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access (Microsoft Access 資料庫引擎)|Office 2010 和 Office 2007|
|Microsoft Access (Microsoft Jet 資料庫引擎)|Office 2007 之前的 Office 版本|

> [!IMPORTANT]
> 您可能必須下載並安裝其他檔案，才能連線至 Access 資料庫。 如需詳細資訊，請參閱此頁面上的[取得連線至 Access 所需的檔案](#officeDownloads)。

 **檔案名稱**  
指定 Access 檔案的路徑和檔案名稱。 例如，本機電腦檔案為 **C:\\MyData.mdb**，或網路共用檔案為 **\\\\Sales\\Database\\Northwind.mdb**。 或按一下 [瀏覽]。 

 >   [!NOTE] 
 > 如果您按一下 [瀏覽] 找到 Access 檔案，則 [開啟] 對話方塊預設會篩選較舊 .MDB 格式和副檔名的檔案。 不過，資料提供者也可以開啟具有較新 .ACCDB 格式和副檔名的檔案。
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出資料庫檔案。  
  
 **User name**  
如果工作群組資訊檔案是與資料庫建立關聯，則請提供有效的使用者名稱。  
  
 **密碼**  
如果工作群組資訊檔案是與資料庫建立關聯，則請在這裡提供使用者的密碼。
 
如果所有使用者都使用單一密碼來保護資料庫，請參閱[資料庫檔案受到密碼保護嗎？](#database_password)。
  
 **進階**  
在 [資料連結屬性] 對話方塊中，指定進階選項 (例如資料庫密碼或非預設工作群組資訊檔案)。  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>我在資料來源清單中看不到 Access
如果您在資料來源清單中看不到 Access，則您正在執行 64 位元精靈嗎？ Excel 和 Access 的提供者一般是 32 位元，而且在 64 位元精靈中看不到。 請改執行 32 位元精靈。

> [!NOTE]
> 若要使用 64 位元版本的 [SQL Server 匯入和匯出精靈]，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，而且只會安裝 32 位元檔案 (包含 32 位元版本的精靈)。

## <a name="officeDownloads"></a>取得連線至 Access 所需的檔案  
您可能必須下載尚未安裝的 Microsoft Office 資料來源 (包含 Access 和 Excel) 的連線元件。 在這裡下載 Access 和 Excel 檔案的連線元件最新版本：[Microsoft Access Database Engine 2016 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
最新版的元件可以開啟舊版 Access 所建立的檔案。

如果電腦有 32 位元版本的 Office，則必須安裝 32 位元版本的元件，而且您也必須確定以 32 位元模式執行套件。

如果您有 Office 365 訂用帳戶，請確定下載 Access Database Engine 2016 可轉散發套件，而非 Microsoft Access 2016 Runtime。 當您執行安裝程式時，可能會看到錯誤訊息，指出您無法使用 Office 隨選即用元件並存安裝下載。 若要略過此錯誤訊息，請開啟 [命令提示字元] 視窗並執行使用 `/quiet` 參數所下載的 .EXE 檔案，以無訊息模式執行安裝。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a> 資料庫檔案受到密碼保護嗎？
在某些情況下，Access 資料庫受到密碼保護，但不使用工作群組資訊檔案。 所有使用者都必須提供相同的密碼，但不需要輸入使用者名稱。 若要提供資料庫密碼，請執行下列動作。

1.  在 [選擇資料來源] 或 [選擇目的地] 頁面上，按一下 [進階] 按鈕以開啟 [資料連結屬性] 對話方塊。  
2.  在 [資料連結屬性] 對話方塊中，選取 [全部] 索引標籤。  
3.  在屬性和值的清單中，選取 [Jet OLEDB:Database 密碼] 。   
    
    ![指定 Access 密碼、畫面 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  按一下 [編輯值] 開啟 [編輯屬性值] 對話方塊。  
    
    ![指定 Access 密碼、畫面 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  在 [編輯屬性值] 對話方塊中，輸入資料庫密碼。
6.  按一下每個對話方塊中的 [確定] 返回精靈的 [選擇資料來源] 或 [選擇目的地] 頁面，並繼續。

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>從 Access 匯出時保留自動編號值
若要允許將來源資料中的現有識別值插入目的地資料表中的識別資料行，請選擇 [資料行對應] 對話方塊的 [啟用識別插入] 選項。 目的地識別欄位一般預設不允許您插入現有值。 若要顯示 [資料行對應] 對話方塊，請在到達精靈的 [選取來源資料表和檢視] 頁面時選取 [編輯對應]。 若要查看這些頁面，請參閱[選取來源資料表和檢視](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)和[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。

如果您現有的主索引鍵位於識別資料行、autonumber 資料行或對等項目內，您通常必須選取此選項來保留現有的主索引鍵值。 否則目的地識別欄位通常會指派新值。

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

