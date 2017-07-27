---
title: "先前 SQL Server Management Studio 版本 | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 87f593c3-8b76-4c12-963a-31d35f2fb294
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: dd279b20fdf0f42d4b44843244aeaf6f19f04718
ms.openlocfilehash: f55f56b31aec2e094a35200e6fe08b28c93affb0
ms.contentlocale: zh-tw
ms.lasthandoff: 07/27/2017

---
# <a name="previous-sql-server-management-studio-releases"></a>先前 SQL Server Management Studio 版本
  
可使用下列舊版 SQL Server Management Studio。

## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-170-releasehttpgomicrosoftcomfwlinklinkid847722"></a>![下載](../ssdt/media/download.png) [SQL Server Management Studio 17.0 版](http://go.microsoft.com/fwlink/?LinkID=847722)

**版本資訊**  
  
*此版本的 SSMS 使用 Visual Studio 2015 獨立模式 Shell。*  
版本號碼：17.0  
此版本的組建編號：14.0.17099.0

## <a name="changelog"></a>變更記錄  

請參閱 [17.0](sql-server-management-studio-changelog-ssms.md#ssms-170-release)。

   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1653-releasehttpgomicrosoftcomfwlinklinkid840946"></a>![下載](../ssdt/media/download.png) [SQL Server Management Studio 16.5.3 版本](http://go.microsoft.com/fwlink/?LinkID=840946)

**版本資訊**  
  
*此版本的 SSMS 使用 Visual Studio 2015 獨立模式 Shell。*  
版本號碼：16.5.3  
此版本的組建編號：13.0.16106.4

## <a name="changelog"></a>變更記錄  

16.5.3

這個版本已修正下列問題：

* 修正 SSMS 16.5.2 中出現的問題，這造成 'Table' 節點會在資料表有多個疏鬆資料行時展開。

* 使用者可以將包含 OData 連線管理員且連線到 Microsoft Dynamics AX/CRM Online 資源的 SSIS 套件部署到 SSIS 目錄。 如需詳細資訊，請參閱 [OData 連線管理員](https://msdn.microsoft.com/library/dn584133.aspx)。

* 在現有資料表上設定 Always Encrypted 失敗，不相關的物件發生錯誤。 [Connect 識別碼 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* 無法為具有多個結構描述的現有資料庫設定 Always Encrypted。 [Connect 識別碼 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* Always Encrypted、加密資料行精靈失敗，原因是資料庫包含參考系統檢視的檢視。 [Connect 識別碼 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* 使用 Always Encrypted 進行加密時，未正確處理加密後來自重新整理模組的錯誤。

* 「開啟最近使用的項目」功能表未顯示最近儲存的檔案。 [Connect 識別碼 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* SSMS 在以右鍵按一下資料表索引時 (透過遠端 (網際網路) 連線) 很緩慢。 [Connect 識別碼 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* 修正 SQL Designer 捲軸的問題。 [Connect 識別碼 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* 資料表的操作功能表會短暫停止回應 
 
* SSMS 有時會擲回活動監視器的例外狀況及損毀。 [Connect 識別碼 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 會損毀，並出現錯誤「處理序因位於 IP 71AF8579 (71AE0000) 的 .NET 執行階段發生內部錯誤而終止，錯誤碼為 80131506」



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-165-releasehttpgomicrosoftcomfwlinklinkid832812"></a>![下載](../ssdt/media/download.png) [SQL Server Management Studio 16.5 版](http://go.microsoft.com/fwlink/?LinkID=832812)

**版本資訊**  
  
*此版本的 SSMS 使用 Visual Studio 2015 獨立模式 Shell。*  
版本號碼：16.5  
本版的組建編號：13.0.16000.28

**此組建的已知問題**  

1. Invoke-Sqlcmd 在 CHECK 條件約束發生時錯誤插入多個資料列。 [Microsoft Connect 項目：811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

2. 建立可用性群組時，非英文語言版本完全無法運作。

3. 按一下查詢計劃 XML，不會開啟適當的 SSMS UI。

**變更記錄**

* 修正了當按一下名稱包含 ";:" 資料庫資料表時會發生當機的問題。
* 修正了在 AS表格式資料庫之 [屬性] 視窗的 [模型] 頁面中執行變更時，會寫出原始定義的問題。 
[Microsoft Connect 項目：3080744](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* 修正了暫存檔案會新增到 [最近使用的檔案] 清單。  
[Microsoft Connect 項目：2558789](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* 修正了物件總管樹狀目錄中，使用者資料表節點之 [管理壓縮] 功能表項目遭到停用的問題。  
[Microsoft Connect 項目：3104616](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* 修正了使用者無法設定物件總管、註冊後的伺服器總管、範本總管與物件總管詳細資料的字型大小問題。 這些總管會使用環境的字型。  
[Microsoft Connect 項目：691432](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* 修正了 SSMS 在連線中斷後，一律時會重新連線到預設資料庫的問題。  
[Microsoft Connect 項目：3102337](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* 修正了原則管理與查詢編器視窗中許多 DPI 太高的問題，包括執行計畫圖示。

* 修正了「擴充的事件」沒有選項可以設定字型與色彩的問題。

* 修正了 SSMS 會在關閉應用程式時，或在嘗試顯示錯誤對話方塊時會損毀時的問題。


   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1641-september-2016-releasehttpgomicrosoftcomfwlinklinkid828615"></a>![下載](../ssdt/media/download.png) [SQL Server Management Studio 16.4.1 (2016 年 9 月) 版](http://go.microsoft.com/fwlink/?LinkID=828615)

**版本資訊**  
  
*此版本的 SSMS 使用 Visual Studio 2015 獨立模式 Shell。*  
版本號碼：16.4.1  
此版本的組建編號：13.0.15900.1
  
**此組建的已知問題**  

1. **使用 Active Directory 通用驗證的 SSMS 執行個體只能以單一 Azure Active Directory 帳戶進行登入。**  
    此限制僅限於 Active Directory 通用驗證。您可以使用 Active Directory 密碼驗證、Active Directory 整合式驗證或 SQL Server 驗證登入不同的伺服器。
    
    因應措施為使用另一個 SSMS 執行個體來以另一個 Azure Active Directory 帳戶進行登入。 
    
2. **Data-Tier Application Framework (DacFx) 命令和 SSMS 中的結構描述設計工具不支援 Active Directory 通用驗證。**  
    使用 DacFx 的命令 (例如匯入與匯出)、SSMS 中的結構描述設計工具，目前並不支援 Active Directory 通用驗證。
    
    因應措施為使用 SSMS 所提供的其他形式驗證：Active Directory 密碼驗證、Active Directory 整合式驗證或 SQL Server 驗證。

3. **SSMS 只能連線到 SQL Server 2016 Integration Services (SSIS 2016) 執行個體。**  
    SQL Server Integration Services 具有會防止連線到先前版本的已知相容性限制。
    
    此問題的因應措施為使用 [與您的 SSIS 執行個體對齊的 SSMS 版本](../ssms/previous-sql-server-management-studio-releases.md)來連線到您的 SQL Server Integration Service 執行個體。 
  
4. **SSMS 不會儲存 SQL Server 2008 R2 和較早 SQL Server 版本的維護計畫。**  
    這是一個我們希望能於未來解決的已知限制。 在此期間，您可以使用 [SSMS 2014 版本](../ssms/previous-sql-server-management-studio-releases.md) 來儲存維護計畫。  
    
5. **非英文的 SSMS 安裝可能需要安裝額外的安全性套件。**  
非英文的 SSMS 語言版本如果安裝在 Windows 8、Windows 7、Windows Server 2012 及 Windows Server 2008 R2，就需要 [KB 2862966 安全性更新程式封裝](https://support.microsoft.com/en-us/kb/2862966) 。
  
6. **如果用戶端電腦上沒有安裝 SQL Server，SQL Server 組態管理員將無法啟動**  
    如果您沒有在用戶端電腦上安裝 SQL Server，並啟動 SQL Server 組態管理員，您將會看見下列錯誤：   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * 如果您已將 SQL Server 執行個體加入 SSMS 中的 [已註冊的伺服器] 清單：  
        1. 瀏覽到 SSMS 中的 [已註冊的伺服器] 檢視。  
        2. 以滑鼠右鍵按一下您想要設定的 SQL Server 執行個體。  
        3. 從右鍵功能表選取 [SQL Server 組態管理員...]。    
          
      * 如果您尚未將 SQL Server 執行個體加入 SSMS 中的 [已註冊的伺服器] 清單：  
        1. 以系統管理員身分開啟命令提示字元。  
        2. 使用下列命令執行 Mofcomp 工具：  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. 執行 Mofcomp 工具之後，請執行下列命令以重新啟動 WMI 服務讓變更生效：  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  

 
**變更記錄** 

*  修正了嘗試變更/修改預存程序失敗的問題︰  
[Microsoft Connect 項目 #3103831](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* 新增加 'Read-SqlTableData'、'Read-SqlViewData' 及 'Write-SqlTableData' Cmdlet，讓您可以使用 PowerShell 檢視及寫入資料。  
[Trello Read-SqlTableData 卡](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Microsoft Connect 項目 #2685363](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* 新增加 'Add-SqlLogin' Cmdlet 可讓您透過 PowerShell 執行一些新的登入管理工作。  
[Microsoft Connect 項目 #2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  連線到境內不同雲端的使用者現在可享有更好的支援與使用經驗。
    
*  修正了擲回記憶體不足例外狀況的問題。  
[Microsoft Connect 項目 #3062914](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Microsoft Connect 項目 #3074856](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  修正了無法使用結構描述作為篩選選項的問題。  
[Microsoft Connect 項目 #3058105](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Microsoft Connect 項目 #3101136](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  修正了無法存取延伸資料庫之 [監視器] 視窗的問題。
    
*  修正了 F1 說明一律會開啟線上內容的問題。 使用者現在可以透過 [說明] 功能表中的 [設定說明偏好]，選擇要使用線上說明或離線說明。   
[Microsoft Connect 項目 #2826366](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  修正了編寫 1200 相容性層級之 Analysis Services 表格式模型的指令碼，仍無法去除編寫指令碼的密碼，而且即使伺服器版本已經是「用戶端模型物件現在會在編寫指令碼之前先同步」亦是如此的問題。
    
*  修正了 'SELECT TOP N ROWS' 選項會產生 TOP 運算子即將被取代之語法的問題。  
[Microsoft Connect 項目 #3065435](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  修正 SSMS 中多項版面配置問題，包括 [登入屬性] 頁面及各項進階查詢執行選項的問題。   
[Microsoft Connect 項目 #3058199](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 項目 #3079122](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 項目 #3071384](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  修正了使用者一開啟新的查詢視窗，就會自動建立解決方案的問題。   
[Microsoft Connect 項目 #2924667](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Microsoft Connect 項目 #2917742](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Microsoft Connect 項目 #2612635](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  修正了當時態表位於系統資料庫時，在物件總管中無法擴充的問題。  
[Microsoft Connect 項目 #2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  已修正 SSMS 在執行批次後對 SELECT @@trancount 執行查詢的問題。    
[Microsoft Connect 項目 #3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  修正了 Analysis Services 在從伺服器的 [屬性] 頁面建立指令碼時，會產生隱藏的連線對話方塊的問題。
    
*  修正了 Ctrl + Q 不會選取 [快速啟動] 工具列的問題。
    
*  修正了使用 [伺服器屬性] 對話方塊，為大於 2 TB 之資料庫變更資料庫的 MaxSize 時，資料庫會中斷的問題。  
[Microsoft Connect 項目 #1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  修正了 [還原資料庫精靈] 不接受包含前置空格之檔案名稱的問題︰   
[Microsoft Connect 項目 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)

*  修正了 [還原資料庫精靈] 不接受包含前置空格之檔案名稱的問題︰   
[Microsoft Connect 項目 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-163-august-2016-releasehttpgomicrosoftcomfwlinklinkid824938"></a>![下載](../ssdt/media/download.png) [SQL Server Management Studio 16.3 (2016 年 8 月) 版](http://go.microsoft.com/fwlink/?LinkID=824938)
 2016 年 8 月 15 日 | 版本號碼：13.0.15700.28

**功能**  
1. 新增驗證選項：Active Directory 通用驗證
2. SQL Server PowerShell 模組新增加的 Cmdlet
3. Database Engine Tuning Advisor (DTA) 與 Extended Events 範本
4. [SSMS 高解析度顯示器](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/)搶鮮版 (Beta) 支援

[如需可用功能的資訊，請參閱 SSMS 變更記錄。](../ssms/sql-server-management-studio-changelog-ssms.md)

**已知問題**

下列為此版本 SQL Server Management Studio 版本的問題與限制：  

1. **使用 Active Directory 通用驗證的 SSMS 執行個體只能以單一 Azure Active Directory 帳戶進行登入。**  
    此限制僅限於 Active Directory 通用驗證。您可以使用 Active Directory 密碼驗證、Active Directory 整合式驗證或 SQL Server 驗證登入不同的伺服器。
    
    因應措施為使用另一個 SSMS 執行個體來以另一個 Azure Active Directory 帳戶進行登入。 
    
2. **Data-Tier Application Framework (DacFx) 命令和 SSMS 中的結構描述設計工具不支援 Active Directory 通用驗證。**  
    使用 DacFx 的命令 (例如匯入與匯出)、SSMS 中的結構描述設計工具，目前並不支援 Active Directory 通用驗證。
    
    因應措施為使用 SSMS 所提供的其他形式驗證：Active Directory 密碼驗證、Active Directory 整合式驗證或 SQL Server 驗證。

3. **SSMS 只能連線到 SQL Server 2016 Integration Services (SSIS 2016) 執行個體。**  
    SQL Server Integration Services 具有會防止連線到先前版本的已知相容性限制。
    
    此問題的因應措施為使用 [與您的 SSIS 執行個體對齊的 SSMS 版本](../ssms/previous-sql-server-management-studio-releases.md)來連線到您的 SQL Server Integration Service 執行個體。 
  
4. **SSMS 不會儲存 SQL Server 2008 R2 和較早 SQL Server 版本的維護計畫。**  
    這是一個我們希望能於未來解決的已知限制。 在此期間，您可以使用 [SSMS 2014 版本](../ssms/previous-sql-server-management-studio-releases.md) 來儲存維護計畫。  
    
5. **非英文的 SSMS 安裝可能需要安裝額外的安全性套件。**  
非英文的 SSMS 語言版本如果安裝在 Windows 8、Windows 7、Windows Server 2012 及 Windows Server 2008 R2，就需要 [KB 2862966 安全性更新程式封裝](https://support.microsoft.com/en-us/kb/2862966) 。
  
6. **如果用戶端電腦上沒有安裝 SQL Server，SQL Server 組態管理員將無法啟動**  
    如果您沒有在用戶端電腦上安裝 SQL Server，並啟動 SQL Server 組態管理員，您將會看見下列錯誤：   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * 如果您已將 SQL Server 執行個體加入 SSMS 中的 [已註冊的伺服器] 清單：  
        1. 瀏覽到 SSMS 中的 [已註冊的伺服器] 檢視。  
        2. 以滑鼠右鍵按一下您想要設定的 SQL Server 執行個體。  
        3. 從右鍵功能表選取 [SQL Server 組態管理員...]。    
          
      * 如果您尚未將 SQL Server 執行個體加入 SSMS 中的 [已註冊的伺服器] 清單：  
        1. 以系統管理員身分開啟命令提示字元。  
        2. 使用下列命令執行 Mofcomp 工具：  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. 執行 Mofcomp 工具之後，請執行下列命令以重新啟動 WMI 服務讓變更生效：  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  


**修正**
1. 修正了在 SSMS 中檢視解密後之 AlwaysEncrypted 大型物件 (LOB) 資料行純文字的錯誤 (Microsoft Connect 項目 #2413024)。
2. 修正了 [永遠加密] 對話方塊中的錯誤，以修正未啟用 Windows 視覺樣式 (例如啟用高對比顯示) 時發生的當機問題。
3. 修正了「找不到方法」錯誤造成無法連線到 SQL Server 執行個體的錯誤。
4. 修正了使用 Datetime Offset 建立資料分割函數時會造成 SSMS 當機的錯誤。
5. 修正了移除啟動 Distributed Replay 管理工具 (DReplay.exe) 需要Microsoft .Net 3.5 的錯誤。
6. 修正了 Analysis Services 部署精靈中的錯誤，以支援完整的伺服器名稱。
7. 修正了在 SSMS 中顯示採用 2016 相容性模型之 Analysis Services 表格式模型的資料分割問題 (Microsoft Connect 項目 #2845053)。

[如需各項修正的資訊，請參閱 SSMS 變更記錄。](../ssms/sql-server-management-studio-changelog-ssms.md)
 
---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-july-2016-hotfix-update-releasehttpgomicrosoftcomfwlinklinkid822301"></a>![下載](../ssdt/media/download.png) [SQL Server Management Studio 2016 年 7 月 Hotfix 更新版本](http://go.microsoft.com/fwlink/?LinkID=822301)

2016 年 7 月 13 日 | 版本號碼：13.0.15600.2

**功能**  
1. 在 SSMS 中支援 Azure SQL 資料倉儲。   
2. SQL Server PowerShell 模組的重大更新。   
3. 大幅改善 Azure SQL 資料庫的連線時間。  
4. 改進 SQL Server 2016 (1200 相容性層級) 表格式資料庫在 Analysis Services 處理對話方塊及許多其他項目上的支援。   

[如需詳細資訊及功能，請查看 SSMS 變更記錄。](../ssms/sql-server-management-studio-changelog-ssms.md)

**已知問題** 
1. **SSMS 7 月 Hotfix 版本的安裝程式會以 SSMS 8 月版本顯示。**
7 月更新 Hotfix 的安裝網頁因內部組建設定之故而顯示為 8 月。 此封裝實為 SSMS 7 月版本的 Hotfix。 
2. **SSMS 在安裝「2016 年 7 月 Hotfix」版本之後便無法連線到 SQL Server 執行個體。**
我們已注意到一項有關最新 SSMS 更新的問題，其中嘗試連線到伺服器將會出現下列錯誤訊息： 
   ```
    "Method not found: 'Void Microsoft.SqlServer.Management.Common.SqlConnectionInfo.set_ApplicationIntent(System.String)'"
    ```
  
    此問題的修正將會在下個 SSMS 版本中提供： 此問題的因應措施為解除安裝並重新安裝 SSMS。 如需詳細資料， [請造訪這個有關該問題的 Microsoft Connect 討論串](https://connect.microsoft.com/SQLServer/feedback/details/2925257/not-able-to-connect-to-sql-server-instances-after-installing-ssms-2016-july-update)。
    
3. **SSMS 會在使用者嘗試選取 Azure 儲存體帳戶時當機。**
SSMS 7 月版本和 7 月 Hotfix 版本會在您嘗試選取 Azure 儲存體帳戶，且沒有「傳統」儲存體帳戶的情況下當機。
此問題的修正將會在即將推出的 SSMS 版本中堤供。 此問題的因應措施為建立傳統儲存體帳戶來將您的資料庫備份/還原到 Azure 儲存體帳戶，或是 [使用 T-SQL 進行備份或還原](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx)。

4. **SSMS 只會在備份/還原精靈中顯示「傳統」Azure 儲存體帳戶。**
SSMS 7 月版本和 7 月 Hotfix 版本在您嘗試使用備份或還原精靈進行備份或還原時，只會針對新憑證建立顯示「傳統」Azure 儲存體帳戶。
此問題的修正將會在即將推出的 SSMS 版本中堤供。 此問題的因應措施為將您的資料庫備份/還原到可用的 Azure「傳統」儲存體帳戶，或是 [使用 T-SQL 進行備份或還原](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx)來備份到「ARM 類型」儲存體帳戶。 

5. **非英文的 SSMS 安裝可能需要安裝額外的安全性套件。**
非英文的 SSMS 語言版本如果安裝在 Windows 8、Windows 7、Windows Server 2012 及 Windows Server 2008 R2，就需要 [KB 2862966 安全性更新程式封裝](https://support.microsoft.com/en-us/kb/2862966) 。
6. **SSMS 只能連線到 SQL Server 2016 Integration Services (SSIS 2016) 執行個體。** SQL Server Integration Services 具有會防止連線到先前版本的已知相容性限制。
此問題的因應措施為使用與您的 SSIS 執行個體對齊的 SSMS 版本來連線到您的 SQL Server Integration Service 執行個體。
7. **SSMS 不會儲存 SQL Server 2008 R2 和較早 SQL Server 版本的維護計畫。** 我們正在努力修正此問題。 在此期間，您可以使用 SSMS 2014 版本及較早版本來儲存維護計畫。
8. **如果用戶端電腦上沒有安裝 SQL Server，SQL Server 組態管理員將無法啟動。** 如果您沒有在用戶端電腦上安裝 SQL Server，並啟動 SQL Server 組態管理員，您將會收到「無法連線到 WMI 提供者」錯誤。 因應措施：
    * 以系統管理員身分開啟命令提示字元。
    * 使用下列命令執行 Mofcomp 工具：  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * 執行 Mofcomp 工具之後，請執行下列命令以重新啟動 WMI 服務讓變更生效：  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**修正**  
1. 修正 SSMS 查詢設計工具中的錯誤，讓沒有 SELECT 權限的使用者也能將資料表加入設計工具中。
2. 修正錯誤，以新增 'TRY_CAST()' 與 'TRY_CONVERT()' 函數的 IntelliSense 支援 [(Microsoft Connect 項目 #2453461)](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast)。
3. 修正 SSMS 編輯器視窗中的錯誤，允許以拖放方式開啟 SQL 檔案 [(Microsoft Connect 項目 #2690658)](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios)。
4. 修正 Analysis Services 的錯誤，為多維度 Analysis Services 模型正確顯示資料摘要提供者。
5. 修正 SSMS 中的問題，防止在嘗試編輯 SSMS 資料表設計工具中的加入連結時當機 [(Microsoft Connect 項目 #2721052)](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms)。  

[如需詳細資訊及錯誤修正，請查看 SSMS 變更記錄。](../ssms/sql-server-management-studio-changelog-ssms.md)

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-june-2016-releasehttpgomicrosoftcomfwlinklinkid799832"></a>![下載](../ssdt/media/download.png) [SQL Server Management Studio 2016 年 6 月版本](http://go.microsoft.com/fwlink/?LinkID=799832)

2016 年 6 月 1 日 | 版本號碼：13.0.15000.23

**功能**  
簡化的新 SSMS 安裝程式。 獨立的 SSMS 版本。 自動檢查更新。 新的 [快速尋找] 對話方塊。 以 Visual Studio 2015 Shell 為基礎建置的 SSMS，以及更多其他內容。   
[如需詳細資訊，請查看 SSMS 變更記錄。](../ssms/sql-server-management-studio-changelog-ssms.md)

**已知問題** 
1. **從永遠加密精靈產生 PowerShell 指令碼的功能目前已停用。**
此問題的修正將會在後續的每月 SSMS 更新中提供。
2. **在您已連線到 Azure SQL Database 時，物件總管中的 [加密資料行] 操作功能表項目將會針對資料表和資料行停用。** 此問題的修正將會在後續的每月 SSMS 更新中提供。 因應措施為在物件總管中以滑鼠右鍵按一下您的資料庫，選取 [工作]，然後選擇 [加密資料行] 以加密 Azure SQL Database 資料行和資料表。
3. **SSMS 只能連線到 SQL Server 2016 Integration Services (SSIS 2016) 執行個體。** SQL Server Integration Services 具有會防止連線到先前版本的已知相容性限制。
此問題的因應措施為使用與您的 SSIS 執行個體對齊的 SSMS 版本來連線到您的 SQL Server Integration Service 執行個體。
4. **SSMS 不會儲存 SQL Server 2008 R2 和較早 SQL Server 版本的維護計畫。** 我們正在努力修正此問題。 在此期間，您可以使用 SSMS 2014 版本及較早版本來儲存維護計畫。
5. **如果用戶端電腦上沒有安裝 SQL Server，SQL Server 組態管理員將無法啟動。** 如果您沒有在用戶端電腦上安裝 SQL Server，並啟動 SQL Server 組態管理員，您將會收到「無法連線到 WMI 提供者」錯誤。 因應措施：
    * 以系統管理員身分開啟命令提示字元。
    * 使用下列命令執行 Mofcomp 工具：  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * 執行 Mofcomp 工具之後，請執行下列命令以重新啟動 WMI 服務讓變更生效：  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**修正**  
1. SSMS 中的 [快速尋找] 對話方塊將能更好地與目前的文件整合，並允許透過規則運算式做出搜尋 ([Microsoft Connect 項目 #2735513](https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/))。
2. 修正 SSMS 即時線上 F1 說明中的錯誤，以正確顯示說明文件和文章。
3. 修正查詢資料存放區 [迴歸查詢] 檢視中，因捲動而造成 SSMS 當機的錯誤。
4. 修正 Excel Analysis Services OLEDB 連接器中的錯誤，以允許從 Excel 2016 連線到 SQL Server Analysis Services。
5. 修正 SSMS [連線] 對話方塊中的錯誤，以在使用多重監視器的系統時，於主要 SSMS 視窗所在的監視器上顯示 [連線] 對話方塊 ([Microsoft Connect 項目 #724909)](https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/)。
6. 修正永遠加密體驗中的錯誤。 已修正 [永遠加密] 功能表選項沒有針對 Stretch Database 正確啟用的錯誤。 同時已修正永遠加密精靈沒有正確使用 SafeNet (Luna SA) HSM 提供者的錯誤。

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2014-sp1httpdownloadmicrosoftcomdownload156156992e6-f7c7-4e55-833d-249bd2348138enux86sqlmanagementstudiox86enuexe"></a>![下載](../ssdt/media/download.png) [SQL Server Management Studio 2014 SP1](http://download.microsoft.com/download/1/5/6/156992E6-F7C7-4E55-833D-249BD2348138/ENU/x86/SQLManagementStudio_x86_ENU.exe)

2015 年 5 月 14 日 | 版本號碼：12.0.4100.1

**功能**  
經改善的 Azure SQL Database 支援，搭配新的在管理入口網站中開啟功能表、資料表設計工具整合以及更多項目。   
[如需詳細資訊，請查看版本資訊](https://support.microsoft.com/en-us/kb/3058865)。

**已知問題**  
不適用

**修正**
1. SSMS 會在維護計畫名稱和第一個 SUB_PLAN 名稱相同的情況下，於移動維護計畫工作期間當機。
2. 您無法針對在 SQL Server Management Studio (SSMS) 中呼叫 sp_executesql 的預存程序進行偵錯。 按下 F11 時，您會收到「物件參考未設定為物件的執行個體」錯誤訊息 ([Microsoft Connect 項目 #736509](https://connect.microsoft.com/SQLServer/feedback/details/736509/sql-server-2012-rtm-management-studio-cannot-debug-sp-executesql))。
3. SSMS 在 SQL Server Express 中不會完全管理全文檢索 ([Microsoft Connect 項目 #740181](https://connect.microsoft.com/SQLServer/feedback/details/740181/management-studio-does-not-fully-manage-full-text-in-sql-server-express))。
4. SSMS 處理編號的預存程序的方式不一致 [(Microsoft Connect 項目 #764197](https://connect.microsoft.com/SQLServer/feedback/details/764197/ssms-2012-inconsistently-handles-numbered-procedures))。
5. SSMS 偶爾會於關閉時當機，並進一步導致它自動重新啟動 ([Microsoft Connect 項目 #774317](https://connect.microsoft.com/SQLServer/feedback/details/774317/sql-server-management-studio-2012-2014-crashes-when-closing))。
6. 在 SSMS 中針對資料行層級權限進行指令碼處理時，建立指令碼會重複陳述式 ([Microsoft Connect 項目 #797967](https://connect.microsoft.com/SQLServer/feedback/details/797967/ssms-create-script-duplicates-the-statements-for-grant-or-deny-column-permissions))。
7. SSMS 可能會在您於工作列上嘗試重新整理 SSMS 視窗圖示時當機 ([Microsoft Connect 項目 #799430](https://connect.microsoft.com/SQLServer/feedback/details/799430/ssms-2012-sp-1-cu-5-installed-crash-when-enforce-refresh-on-connect))。

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2012-sp3httpdownloadmicrosoftcomdownloadf67f673709c-d371-4a64-8bf9-c1dd73f60990enux86sqlmanagementstudiox86enuexe"></a>![下載](../ssdt/media/download.png) [SQL Server Management Studio 2012 SP3](http://download.microsoft.com/download/F/6/7/F673709C-D371-4A64-8BF9-C1DD73F60990/ENU/x86/SQLManagementStudio_x86_ENU.exe)  
  
2015 年 11 月 21 日 | 版本號碼：11.0.6020.0

**功能**  
全功能 SSMS express 版本。 程式碼片段。 資料行存放區索引，以及更多項目。  
[如需詳細資訊，請查看版本資訊。](https://support.microsoft.com/en-us/kb/3072779)
 
**已知問題**  
不適用

**修正**
1. 在您使用匯入和匯出精靈匯入資料時，遺失的資料行無法在錯誤訊息中表示。
2. 當您在 SSMS 中還原差異備份時，出現「無法建立還原計畫，因為 LSN 鏈結中斷」錯誤

---
## <a name="additional-downloads"></a>其他下載  
如需所有 SQL Server Management Studio 的下載清單，請搜尋 [Microsoft 下載中心](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending)。  
  
若要取得最新版的 SQL Server Management Studio，請參閱[下載 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)。  

---  
## <a name="related-resources"></a>相關資源
[Microsoft SQL Server 的更新中心](https://technet.microsoft.com/sqlserver/ff803383.aspx)   
[SQL Server Management Studio 快速入門](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio 論壇](https://social.msdn.microsoft.com/forums/en-us/home?forum=sqltools)  

  

