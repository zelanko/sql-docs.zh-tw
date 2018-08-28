---
title: SQL Server 2008 R2 SP2 版本資訊 | Microsoft Docs
ms.prod: sql
ms.technology: install
ms.custom: ''
ms.date: 01/31/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2008 R2 SP2
- Release Notes, SQL Server 2008 R2 SP2
ms.assetid: e2bd3de7-674c-4ea7-8d53-bb40bba86fae
author: craigg-msft
ms.author: craigg
manager: jhubbard
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: d57f8ffc3d6fb9d1bd85bfa96f4ba431dd7fb114
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "42775844"
---
# <a name="sql-server-2008-r2-sp2-release-notes"></a>SQL Server 2008 R2 SP2 Release Notes
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
這份版本資訊文件將描述有關您安裝或疑難排解 Microsoft SQL Server 2008 R2 Service Pack 2 之前應該閱讀的已知問題。 這份版本資訊文件適用於 SQL Server 2008 R2 SP2 的所有版本，而且僅在線上提供使用。 將定期進行更新。  
  
## <a name="10-whats-new-in-service-pack-2"></a>1.0 Service Pack 2 中的新功能  
新增動態管理檢視 (DMV) **sys.dm_db_stats_properties**。 您可以使用這個 DMV，傳回目前資料庫中所指定之資料表或索引檢視表的統計資料屬性。 例如，這個 DMV 會傳回取樣的資料列數目以及長條圖中的步驟數目。  
  
## <a name="20-before-you-install"></a>2.0 安裝之前  
如需有關如何安裝 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 更新的詳細資訊，請參閱 [SQL Server 2008 R2 服務文件](http://msdn.microsoft.com/library/dd638062(SQL.105).aspx)。  
  
如需有關如何開始使用並安裝 SQL Server 2008 R2 的一般資訊，請參閱 SQL Server 2008 R2 讀我檔案。 安裝媒體中提供此讀我檔案文件。 您也可以在 [SQL Server 線上叢書](sql-server-technical-documentation.md) 和 [SQL Server 論壇](http://social.msdn.microsoft.com/Forums/category/sqlserver/)中尋找更多資訊。  
  
### <a name="21-choose-the-correct-file-to-download-and-install"></a>2.1 選擇要下載並安裝的正確檔案  
您可以使用下表來決定要下載並安裝的檔案。 在安裝 Service Pack 之前，請先確認您擁有正確的系統需求。 系統需求會列在資料表中所連結的下載頁面。  
  
|如果您目前安裝的版本是...|而您要...|請下載並安裝...|  
|-------------------------------------------|----------------------|---------------------------|  
|32 位元版本的任何版本 SQL Server 2008 R2 或 SQL Server 2008 R2 SP1|升級至 32 位元版本的 SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|32 位元版本的 SQL Server 2008 R2 RTM Express 或 SQL Server 2008 R2 SP1 Express|升級至 32 位元版本的 SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 (包括 SQL Server 2008 R2 Management Studio) 之 32 位元版本的用戶端和管理能力工具|將用戶端和管理能力工具升級至 32 位元版本的 SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|32 位元版本的 SQL Server 2008 R2 Management Studio Express 或 SQL Server 2008 R2 SP1 Management Studio Express|升級至 32 位元版本的 SQL Server 2008 R2 SP2 Management Studio Express|SQLManagementStudio_x86_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251791)|  
|32 位元版本的 SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 任何版， **以及** 32 位元版本的用戶端和管理能力工具 (包括 SQL Server 2008 R2 RTM Management Studio)|將所有產品升級至 32 位元版本的 SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|[Microsoft SQL Server 2008 R2 RTM 功能套件](http://www.microsoft.com/download/en/details.aspx?id=16978)中一個或多個 32 位元版本的工具|將工具升級至 32 位元版本的 Microsoft SQL Server 2008 R2 SP2 功能套件|[Microsoft SQL Server 2008 R2 SP2 功能套件](http://go.microsoft.com/fwlink/?LinkId=251792)中一個或多個檔案|  
|無 32 位元版本的 SQL Server 2008 R2 安裝|安裝 Server 2008 R2，包括 SP2|移至 [SQL Server 2008 R2 SP2 – Express Edition](http://go.microsoft.com/fwlink/?LinkId=251791) 並依照指示執行。|  
|無 32 位元版本的 SQL Server 2008 R2 Management Studio 安裝|安裝 SQL Server 2008 R2 Management Studio，包括 SP2|SQLManagementStudio_x86_ENU.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251791) ，可供免費安裝 SQL Server 2008 R2 SP2 Management Studio Express Edition。|  
|64 位元版本的 SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 任何版|升級至 64 位元版本的 SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU 或 SQLServer2008R2SP2-KB2630455-IA64-ENU.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|64 位元版本的 SQL Server 2008 R2 RTM Express 或 SQL Server 2008 R2 SP1 Express|升級至 64 位元版本的 SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe 或 SQLServer2008R2SP2-KB2630455-IA64-ENU.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 (包括 SQL Server 2008 R2 Management Studio) 之 64 位元版本的用戶端和管理能力工具|將用戶端和管理能力工具升級至 64 位元版本的 SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe 或 SQLServer2008R2SP2-KB2630455-IA64-ENU.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|64 位元版本的 SQL Server 2008 R2 Management Studio Express 或 SQL Server 2008 R2 SP1 Management Studio Express|升級至 64 位元版本的 SQL Server 2008 R2 SP2 Management Studio Express|SQLManagementStudio_x64_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251791)|  
|64 位元版本的 SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 任何版， **以及** 64 位元版本的用戶端和管理能力工具 (包括 SQL Server 2008 R2 RTM Management Studio)|將所有產品升級至 64 位元版本的 SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|[Microsoft SQL Server 2008 R2 RTM 功能套件](http://www.microsoft.com/download/en/details.aspx?id=16978)中一個或多個 64 位元版本的工具|將工具升級至 64 位元版本的 Microsoft SQL Server 2008 R2 SP2 功能套件|[Microsoft SQL Server 2008 R2 SP2 功能套件](http://go.microsoft.com/fwlink/?LinkId=251792)中一個或多個檔案|  
|無 64 位元版本的 SQL Server 2008 R2 安裝|安裝 Server 2008 R2，包括 SP2|移至 [SQL Server 2008 R2 SP2 – Express Edition](http://go.microsoft.com/fwlink/?LinkId=251791) 並依照指示執行。|  
|無 64 位元版本的 SQL Server 2008 R2 Management Studio 安裝|安裝 SQL Server 2008 R2 Management Studio，包括 SP2|SQLManagementStudio_x64_ENU.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=251791) ，可供免費安裝 SQL Server 2008 R2 SP2 Management Studio Express Edition。|  
  
### <a name="22-setup-might-fail-if-sqagtresdll-is-locked-by-another-process"></a>2.2 如果 SQAGTRES.dll 已由其他處理序鎖定，安裝程式可能發生失敗  
**問題**：SQL Server 安裝程式作業可能會失敗並出現以下錯誤： `Upgrading of cluster resource C:\Program Files\Microsoft SQL Server\MSSQL10_50.<Instance name>\MSSQL\Binn\SQAGTRES.DLL on machine <Computer name> failed with Win32Exception. Please look at inner exception for details.` 起因是 C:\Windows\system32\SQAGTRES.DLL 已由另一個處理序鎖定，而安裝程式無法加以更新。  
  
**因應措施**：暫時將 C:\Windows\system32\SQAGTRES.DLL 重新命名，例如 C:\Windows\system32\SQAGTRES_old.DLL，然後選取安裝程式錯誤訊息上的 [重試] 選項。 如此，安裝程式就能繼續執行。 重新開機之後，您可以刪除暫存檔 C:\Windows\system32\SQAGTRES_old.DLL。  
  
## <a name="30-known-issues-fixed-in-this-service-pack"></a>3.0 這個 Service Pack 所修正的已知問題  
如需這個 Service Pack 所修正之錯誤和已知問題的完整清單，請參閱這份 [主要知識庫文件](http://support.microsoft.com/kb/2630455)。  
  
## <a name="see-also"></a>另請參閱  
[如何判斷 SQL Server 的版本](http://support.microsoft.com/kb/321185)  
  
