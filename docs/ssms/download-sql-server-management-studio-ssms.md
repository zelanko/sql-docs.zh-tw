---
title: "下載 SQL Server Management Studio (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 04/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安裝 ssms, 下載 ssms, 最新的 ssms"
- Transact-SQL
- ssms.exe
- sql man studio
- sql management studio
- sql management studio install
- download sql management studio
- ms sql management studio
- install sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cc827737cec19c11d2102f968dc2b8bc638bda86
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>下載 SQL Server Management Studio (SSMS)
SQL Server Management Studio (SSMS) 是一個整合式環境，您可以加以利用來存取、設定、管理及開發 SQL Server 的所有元件。 SSMS 利用許多豐富的指令碼編輯器來合併一群非常廣泛的圖形工具，使所有技術層級的開發人員及管理員都能夠存取。 此版除了提升與舊版 SQL Server 之間的相容性之外，也改進了獨立 Web 安裝程式，以及 SSMS 中，當有新版本可用時的快顯通知。  

    
| ![下載這篇文章](../ssdt/media/download.png) 下載 SQL Server Management Studio (SSMS)  |  |
|:---|:---|
|**[下載 SQL Server Management Studio (16.5.3)](https://go.microsoft.com/fwlink/?LinkID=840946)**|供生產環境使用的目前版本。|
|**[下載 SQL Server Management Studio - 候選版 (17.0 RC3)](../ssms/sql-server-management-studio-ssms-release-candidate.md)**|包含對 SQL Server vNext CTP1.3 的支援，並能搭配 16.x 運作，但不建議用於生產環境。| 


> [!NOTE]
> SSMS 的版本現在將以數值標註，而不是以月份。 SSMS 是免費的！ 不需要授權即可安裝和使用。  


## <a name="sql-server-management-studio"></a>Transact-SQL   
**版本資訊**  
  
版本號碼：16.5.3  
此版本的組建編號：13.0.16106.4
  
**支援的 SQL Server 版本**  
  
* 此版本的 SSMS 適用於所有 [支援的 SQL Server 版本 (SQL Server 2008 - SQL Server 2016)，](https://support.microsoft.com/en-us/lifecycle?C2=1044) 並提供最高層級的支援，而能夠使用 Azure SQL Database 中最新的雲端功能及 Azure SQL Data 倉儲。  
* SQL Server 2000 或 SQL Server 2005 並未受到明確限制，但有些功能可能無法正常運作。  
* 此外，SSMS 16.x 版本或 SSMS 2016 可與舊版 SSMS 2014 及更早版本並存安裝。 
  
**支援的作業系統**  
  
搭配最新推出的服務套件使用時，這一版 SSMS 支援下列平台：   
 Windows 10、Windows 8、Windows 8.1、Windows 7 (SP1)、 Windows Server 2012 (64 位元) Windows Server 2012 R2 (64 位元)、Windows Server 2008 R2 (64 位元)  
   
 **可用語言**  
> [!NOTE]  
> 非英文的 SSMS 語言版本如果安裝在 Windows 8、Windows 7、Windows Server 2012 及 Windows Server 2008 R2，就需要 [KB 2862966 安全性更新程式封裝](https://support.microsoft.com/en-us/kb/2862966) 。 
  
 此版 SSMS 提供下列語言版本：  
[中文 (中華人民共和國)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [中文 (台灣)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [英文 (美國)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [法文](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)  
[德文](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [義大利文](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [日文](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [韓文](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [葡萄牙文 (巴西)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [俄文](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [西班牙文](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)  

 
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





如需完整功能清單，請參閱   
                [SQL Server Management Studio - 變更記錄 (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)  
  
若要查看已知問題及解決方法的清單，請參閱   
                [SQL Server Management Studio -  版本資訊](../ssms/sql-server-management-studio-release-notes.md)  
  
如需使用量資料收集的相關資訊，請參閱   
                [SQL Server 隱私權聲明](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx)。  
  
## <a name="previous-releases"></a>舊版  
[先前 SQL Server Management Studio 版本](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>意見反應  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 用戶端工具論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 記錄問題或建議](https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另請參閱  
[教學課程：SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio 文件](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[其他的更新與 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  



