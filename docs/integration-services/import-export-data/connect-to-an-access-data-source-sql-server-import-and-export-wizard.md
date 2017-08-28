---
title: "連接到 Access 資料來源 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 71bb3914e31259bc95a1116c2db03708c0442e8c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>連接到 Access 資料來源 （SQL Server 匯入和匯出精靈）
本主題說明如何連接到**Microsoft Access**資料來源從**選擇資料來源**或**選擇目的地**SQL Server 匯入和匯出精靈 頁面。

下列螢幕擷取畫面顯示 Microsoft Access 資料庫的連接範例。 在此範例中，您不必輸入使用者名稱和密碼，因為目標資料庫不會使用工作群組資訊檔案。

![連接到 Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>若要指定的選項

> [!NOTE]
> 連接選項，此資料提供者存取您的來源或目的地是否都相同。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

**資料來源**  
Microsoft Access 資料提供者的清單可能包含數個項目。 選取最新安裝的版本或對應於建立資料庫檔案的 Access 版本的版本。

|資料來源|Office 版本|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access （Microsoft Access 資料庫引擎）|Office 2010 和 Office 2007|
|Microsoft Access (Microsoft Jet Database Engine)|早於 Office 2007 office 版本|

> [!IMPORTANT]
> 您可能要下載並安裝其他要連接到 Access 資料庫檔案。 請參閱[取得的檔案，您需要連接到 Access](#officeDownloads)在此頁面上，如需詳細資訊。

 **檔案名稱**  
指定存取檔案的路徑和檔案名稱。 例如， **c:\\MyData.mdb**本機電腦上的檔案或 **\\\\銷售\\資料庫\\northwind.mdb 所需**網路共用上的檔案。 或按一下 [瀏覽]。 

 >   [!NOTE] 
 > 如果您按一下**瀏覽**存取檔案，找出**開啟**對話方塊方塊篩選具有較舊的檔案。MDB 格式與檔案副檔名預設。 不過此資料提供者也可以開啟檔案的較新。ACCDB 格式與檔案副檔名。
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出資料庫檔案。  
  
 **使用者名稱**  
如果工作群組資訊檔案與資料庫相關聯，請提供有效的使用者名稱。  
  
 **密碼**  
如果工作群組資訊檔案與資料庫相關聯，提供此使用者的密碼。
 
如果受保護資料庫的所有使用者的單一密碼，請參閱[受到密碼保護的資料庫檔案嗎？](#database_password)。
  
 **進階**  
在 [指定進階的選項，例如資料庫密碼或非預設的工作群組資訊檔案，**資料連結屬性**] 對話方塊。  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>我沒看到存取清單中的資料來源
如果您沒有看到存取資料來源的清單中，您會執行 64 位元精靈嗎？ Excel 和 Access 的提供者是一般的 32 位元和 64 位元精靈 中看不到。 請改為執行 32 位元精靈。

> [!NOTE]
> 若要使用 64 位元版本的 SQL Server 匯入和匯出精靈，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，並只安裝 32 位元檔案，包括 32 位元版本的精靈。

## <a name="officeDownloads"></a>取得連接到存取所需的檔案  
您可能要下載 Microsoft Office 的資料來源，包括 Access 和 Excel，如果它們尚未安裝連接元件。 下載最新版的連線元件，以下 Access 和 Excel 檔案： [Microsoft Access 資料庫引擎 2016年可轉散發套件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
最新版本的元件可以開啟檔案的存取權限的較早版本所建立的。

如果電腦有 32 位元版本的 Office，則必須安裝 32 位元版本的元件，而且您也必須確定您在 32 位元模式執行封裝。

如果您有 Office 365 訂閱，請確定您在 Access 資料庫引擎 2016年可轉散發套件並不使用 Microsoft Access 2016 執行階段時下載。 當您執行安裝程式時，您可能會看到錯誤訊息，您無法安裝下載的並存 Office 按一下來執行元件。 略過此錯誤訊息，以執行安裝以無訊息模式開啟命令提示字元視窗並執行。下載的 EXE 檔案`/quiet`切換。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a>有密碼保護的資料庫檔案嗎？
在某些情況下，有密碼保護 Access 資料庫，但不使用工作群組資訊檔案。 所有使用者必須提供相同的密碼，但不需要輸入使用者名稱。 若要提供資料庫密碼，執行下列作業。

1.  在**選擇資料來源**或**選擇目的地**頁面上，按一下**進階** 按鈕以開啟**資料連結屬性** 對話方塊。  
2.  在**資料連結屬性**對話方塊中，選取**所有** 索引標籤。  
3.  在屬性和值的清單中選取**Jet OLEDB:Database 密碼**。   
    
    ![指定存取密碼，畫面 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  按一下**編輯值**開啟**編輯屬性值** 對話方塊。  
    
    ![指定存取密碼，螢幕 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  在**編輯屬性值**對話方塊方塊中，輸入資料庫密碼。
6.  按一下**[確定]**中每個對話方塊，以返回**選擇資料來源**或**選擇目的地**精靈頁面，並繼續。

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>當您從存取匯出保留 autonumber 值
若要讓現有的識別值要插入至目的地資料表中識別資料行的來源資料中，選擇 [**啟用識別插入**選項**資料行對應**] 對話方塊。 根據預設，目的地識別欄位通常不會讓您插入現有的值。 若要顯示**資料行對應**對話方塊中，選取**編輯對應**到達**選取來源資料表和檢視**精靈頁面。 若要查看這些頁面，請參閱[選取來源資料表和檢視](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)和[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。

如果您現有的主索引鍵位於識別資料行、autonumber 資料行或對等項目內，您通常必須選取此選項來保留現有的主索引鍵值。 否則目的地識別欄位通常會指派新值。

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


