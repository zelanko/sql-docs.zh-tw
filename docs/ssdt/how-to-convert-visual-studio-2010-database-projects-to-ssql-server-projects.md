---
title: 如何：將 Visual Studio 2010 資料庫專案轉換成 SQL Server 資料庫專案並重定目標為不同平台 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.projectconversion.dialog
- sql.data.tools.ImportDAC
ms.assetid: 7e5acf94-5c46-44c7-9ff5-ca7926f5332a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5853dcc142dbee73846617fc3c32e876978f6609
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398571"
---
# <a name="how-to-convert-a-visual-studio-2010-database-projects-to-sql-server-database-projects-and-retarget-to-a-different-platform"></a>HOW TO：將 Visual Studio 2010 資料庫專案轉換成 SQL Server 資料庫專案並重定目標為不同平台
在 SQL Server Data Tools (SSDT) 中，您可以將 Visual Studio 2010 中建立的現有 SQL Server 資料庫、CLR 物件和資料層應用程式專案轉換成新的 SQL Server 資料庫專案。 如此一來，您便能利用 SSDT 提供的新型態資料庫開發體驗，例如更新的 Transact\-SQL 編輯體驗，以及透過程式碼驗證將專案目標重定為 Microsoft SQL Server 2012 和 SQL Azure 的功能。 轉換程序會轉換 SSDT 中具有對等類型的物件 (資料表、檢視表、預存程序、屬性檔或指令碼)，包括物件的權限和 DAC 原則檔。 在轉換記錄檔/報告中將重點強調無法轉換的成品。  
  
下表列出 SSDT 可以或無法轉換的所有專案成品。  
  
|可以轉換的專案成品|無法轉換的專案成品|  
|-------------------------------------------|----------------------------------------------|  
|專案檔<br /><br />.dbproj (Visual Studio 2010 資料庫和伺服器專案、資料層應用程式專案) 專案檔<br /><br />.csproj 和 .vbproj CLR 專案檔可以轉換，但可能會造成資料遺失|資料庫單元測試專案<br /><br />部分專案，例如 .files 項目|  
|屬性檔<br /><br />*.sqldeployment、.sqlsettings 和 .sqlpolicy 檔會轉換成對應的專案屬性頁<br /><br />.sqlpermissions 檔會轉換成 Transact\-SQL 指令碼|專案屬性<br /><br />Server.sqlsettings<br /><br />.sqlcmd 檔案中定義的 SQLCMD 變數|  
|.sql 檔是以現有資料夾結構匯入的。|擴充性檔案。|  
|預先部署和部署後指令碼|在專案轉換後，資料庫參考將需要手動重新建立。|  
|結構描述比較檔|資料產生檔。|  
  
### <a name="to-convert-a-project"></a>若要轉換專案  
  
1.  開啟 SQL Server 2005 或 2008 資料庫專案。  
  
2.  [轉換成 SQL Server 資料庫專案] 精靈隨即自動開啟。 選取 [轉換成 SQL Server 資料庫專案]，然後按一下 [確定]。 保留預設值，以備份選取的現有檔案。  
  
3.  自動產生轉換報告，列出所有已經轉換的檔案。 若要閱讀有關轉換程序的詳細資訊，按一下專案檔名旁邊的 **+** 號。  
  
4.  請注意，[方案總管] 中的專案檔、屬性檔和結構描述物件全部都會轉換。  
  
### <a name="to-change-a-projects-target-platform"></a>變更專案的目標平台  
  
1.  以滑鼠右鍵按一下 [方案總管] 中新轉換的專案，再選取 [屬性] 存取 [專案設定] 對話方塊。  
  
2.  從 [目標平台] 下拉式清單中選取 SSDT 支援的任何平台。  
  
## <a name="see-also"></a>另請參閱  
[如何：變更目標平台及發行資料庫專案](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)  
  
