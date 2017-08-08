---
title: "下載 SQL Server Management Studio (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 06/27/2017
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
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: dcb3ee622bac9c70a235e1ff124f7041549825c0
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>下載 SQL Server Management Studio (SSMS)
SQL Server Management Studio (SSMS) 是整合式環境，可用於管理任何 SQL 基礎結構，從 SQL Sever 到 SQL Database 皆適用。 SSMS 提供工具讓您可以從您部署的位置設定、監視及管理 SQL 執行個體。 您可使用 SSMS 部署、監視以及升級應用程式所使用的資料層元件，以及建置查詢和指令碼。 

此版除了提升與舊版 SQL Server 之間的相容性之外，也改進了獨立 Web 安裝程式，以及 SSMS 中，當有新版本可用時的快顯通知。  
  
免費![下載](../ssdt/media/download.png) SSMS！ **[下載 SQL Server Management Studio 17.1](https://go.microsoft.com/fwlink/?linkid=849819)** SSMS 17.X 是最新一代的 SQL Server Management Studio，支援 SQL Server 2017。 

![下載](../ssdt/media/download.png) **[下載 SQL Server Management Studio 17.1 升級套件 (從 17.0 升級到 17.1)](https://go.microsoft.com/fwlink/?linkid=849821)**

> [!NOTE]
> SQL Server PowerShell 模組現在透過 PowerShell 資源庫個別安裝。  如需詳細資訊，請參閱[下載指示](download-sql-server-ps-module.md)。

## <a name="sql-server-management-studio"></a>Transact-SQL   
**版本資訊**  
  
版本號碼：17.1  
此版本的組建編號：14.0.17119.0

## <a name="new-in-this-release"></a>此版本中的新功能  

SSMS 17.1 是 SQL Server Management Studio 17.X 世代的第一項更新。  17.X 世代提供 SQL Server 2008 到 SQL Server 2017 幾乎所有功能領域的支援。  17.X 版本也是支援 SQL Analysis Service PaaS 的 SSMS 世代。

17.1 版本包括：

* 修正數個使用者回報的問題 
* 新的 Integration Services 向外延展管理工具

如需完整變更清單，請參閱   
                [SQL Server Management Studio - 變更記錄 (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)  
   
如需使用量資料收集的相關資訊，請參閱   
                [SQL Server 隱私權聲明](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx) 
  
## <a name="supported-sql-offerings"></a>支援的 SQL 供應項目
  
* 此版本的 SSMS 適用於所有[支援的 SQL Server 2008 - SQL Server 2017 版本](https://support.microsoft.com/lifecycle?C2=1044)，並提供最高層級的支援以使用 Azure SQL Database 中最新的雲端功能，以及 Azure SQL 資料倉儲。  
* SQL Server 2000 或 SQL Server 2005 並未受到明確限制，但有些功能可能無法正常運作。  
* 此外，SSMS 17.X 可以與 SSMS 16.X 或 SQL Server 2014 SSMS 及更早的版本並存安裝。 
  
## <a name="supported-operating-systems"></a>支援的作業系統
  
搭配最新推出的服務套件使用時，這一版 SSMS 支援下列 64 位元平台：
- Windows 10 (64 位元)
- Windows 8.1 (64 位元)
- Windows 8 (64 位元)
- Windows 7 (SP1) (64 位元)
- Windows Server 2016
- Windows Server 2012 R2 (64 位元)
- Windows Server 2012 (64 位元)
- Windows Server 2008 R2 (64 位元)

>[!NOTE]
>SSMS 17.X 以 Windows Server 2016 之前發行的 Visual Studio 2015 獨立模式 Shell 為基礎。 Microsoft 重視應用程式相容性，並確保已出貨的應用程式會持續在最新的 Windows 版本上執行。 為了將在 Windows Server 2016 上執行 SSMS的問題降至最低，請確定 SSMS 已套用所有最新的更新。 如果在 Windows Server 2016 上發生任何 SSMS 問題，請連絡支援服務。 支援小組會判斷問題是否與 SSMS、Visual Studio 或 Windows 相容性有關。 然後，支援小組會將問題傳送至適當的小組以進行進一步的調查。

## <a name="ssms-installation-tips-and-issues"></a>SSMS 安裝祕訣與問題

>[!NOTE]
> SSMS 17.x 安裝不會升級或取代舊版的 SSMS。  SSMS 17.x 會與舊版並存安裝，使兩個版本同時可供使用。
> 如果電腦中包含並存安裝的 SSMS，請確認已針對您的特定需求啟動正確的版本。
>  ![SSMS 17.x](media/ssms-start-menu.png)

**最小化安裝重新開機**
- 請採取下列動作，以降低 SSMS 安裝程式需要在安裝結束時重新開機的機會：
  - 請確定您執行的是最新版的 Visual C++ 2013 可轉散發套件。 需要 12.00.40649.5 版本 (或更新版本)。 只需要 x64 版本。
  - 請確認電腦上的 .NET Framework 版本是 4.6.1 (或更新版本)。
  - 關閉電腦上開啟的所有其他 Visual Studio 執行個體。
  - 請確定電腦上安裝了所有最新的作業系統更新。
  - 所述的動作通常只需要執行一次。 只有極少數的情況，需要在另外升級至相同主要版本的 SSMS 時重新開機。 針對次要升級，電腦上會安裝好所有的 SSMS 先決條件。

- 若要查看已知問題和解決方法的清單，請參閱 [SQL Server Management Studio - 版本資訊](../ssms/sql-server-management-studio-release-notes.md)。

## <a name="available-languages"></a>可用語言  
> 非英文的 SSMS 語言版本如果安裝在 Windows 8、Windows 7、Windows Server 2012 及 Windows Server 2008 R2，就需要 [KB 2862966 安全性更新程式封裝](https://support.microsoft.com/en-us/kb/2862966) 。 
  
此版 SSMS 提供下列語言版本：

SQL Server Management Studio 17.1：<br>
[中文 (中華人民共和國)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [中文 (台灣)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

SQL Server Management Studio 17.1 升級套件 (從 17.0 升級到 17.1)：<br>
[中文 (中華人民共和國)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x804) | [中文 (台灣)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40a)

## <a name="previous-releases"></a>舊版  
[先前 SQL Server Management Studio 版本](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>意見反應  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 用戶端工具論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 記錄問題或建議](https://connect.microsoft.com/SQLServer/Feedback)  
  
## <a name="see-also"></a>另請參閱  
[教學課程：SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio 文件](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[其他的更新與 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  

