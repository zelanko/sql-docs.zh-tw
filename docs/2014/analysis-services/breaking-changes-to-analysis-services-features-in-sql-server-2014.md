---
title: SQL Server 2014 中 Analysis Services 功能的重大變更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- breaking changes [Analysis Services]
- upgrading Analysis Services
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65b70cf2bb85bca60a372f09a5d3fc9ffedb90cc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66064423"
---
# <a name="breaking-changes-to-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014 中 Analysis Services 功能的重大變更
  本主題描述 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]中的重大變更。 這些變更可能會中斷以舊版 SQL Server 為基礎的應用程式、指令碼或功能。  
  
 本主題內容：  
  
-   [SQL Server 2014 的最新變更](#bkmk_sql2014)  
  
-   [SQL Server 2012 SP1 中的重大變更](#bkmk_2012Sp1)  
  
-   [SQL Server 2012 的最新變更](#bkmk_sql11)  
  
-   [SQL Server 2008/SQL Server 2008 R2 中的重大變更](#bkmk_sql10)  
  
##  <a name="bkmk_sql2014"></a>中的重大變更[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 此版本中的多維度、表格式、資料採礦或 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 功能未宣告任何新的重大變更。  不過，因為  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 很類似 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 版本，所以在此為您提供這兩個舊版的重大變更，以便您從 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]升級。  
  
##  <a name="bkmk_2012Sp1"></a>SQL Server 2012 SP1 中的重大變更  
 全球化相關的程式碼變更也會中斷某些應用程式。 已知問題包括：  
  
 **物件識別碼的區分大小寫**  
 目的是使所有物件識別碼不區分大小寫的程式碼變更，對某些語言具有相反效果。 目的是使所有的物件識別碼不區分大小寫，不論定序為何。 這項變更會將 Analysis Services 與通常用於相同解決方案組的其他應用程式一致。  
  
 針對基於基本拉丁字母 26 個字元的語言，物件識別碼現在不區分大小寫，這是預期的行為。  
  
 對於斯拉夫文和使用大小寫慣例的其他雙制度語言指令碼 (希臘文、亞美尼亞文和科普特文)，物件識別碼現在則區分大小寫。 當物件識別碼和參考之間有大小寫差異時，最有可能發生重大變更 (例如，全使用小寫參考物件識別碼的處理指令碼)。 此行為可能在未來變更，但做為這個問題的暫時解決辦法，我們建議您修改指令碼，以使用與物件識別碼相同的大小寫。  
  
##  <a name="bkmk_sql11"></a>中的重大變更[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 本章節記載針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]功能所報告的重大變更。  
  
|問題|描述|  
|-----------|-----------------|  
|已針對 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 安裝移除安裝命令。|安裝程式會安裝 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]，但是不再設定。 現在已經移除用於組態動作之收集值的安裝命令。 其中包括 /FARMACCOUNT、/FARMPASSWORD、/PASSPHRASE 和 /FARMADMINPORT。<br /><br /> 如果您已經針對自動安裝建立安裝指令碼，您需要為 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 安裝修改這些指令碼。 替代方法是使用 PowerShell 指令程式，在自動安裝模式下設定伺服器。 如需詳細資訊，請參閱[使用 Windows PowerShell](power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)[從命令提示字元安裝 powerpivot](../../2014/sql-server/install/install-powerpivot-from-the-command-prompt.md)和 powerpivot 設定。|  
  
##  <a name="bkmk_sql10"></a>中的重大變更[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]/[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
 本章節包含舊版的重大變更。 如果您是從 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]升級，則應該檢閱 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]中導入的重大變更。  
  
|問題|描述|  
|-----------|-----------------|  
|shallow exists 函數現在會以不同的方式使用包含列舉集之列舉成員或交叉聯結的命名集。|在 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]中，shallow exists 函數不會使用包含列舉集之列舉成員或交叉聯結的命名集。 若要與原始發行版本和 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]SP1 相容，請將組態屬性 "ConfigurationSettings\OLAP\Query\NamedSetShallowExistsMode" 設定為 1。若要與 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] SP2 相容，請將它設定為 2。|  
|VBA 函數處理 Null 值和空白值的方式與 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] 中的處理方式不同|在 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]中，當 Null 值或空白值當做引數使用時，VBA 函數原本會傳回 0 或空字串。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]中，它們將會傳回 Null。|  
|移轉精靈將會失敗，因為 DSO 依預設並未安裝。|依預設，SQL Server 2008 並不會安裝 DSO (決策支援物件) 回溯相容性元件。 回溯相容性封裝依預設會安裝，但該封裝的 DSO 元件將會停用。 因為 SQL Server Analysis Services 移轉精靈相依於這個元件，所以除非安裝這個元件，否則此精靈將會失敗。 若要安裝 DSO 元件，請執行下列動作：<br /><br /> 1）開啟 [控制台]。<br />2）在 Windows XP 或 Windows Server 2003 中，選取 [**新增或移除程式**]。 在 Windows Vista 和 Windows Server 2008 中選取 **[程式和功能]**。<br />3）以滑鼠右鍵按一下 [ **Microsoft SQL Server 2005 回溯相容性**]，然後選取 [**變更**]。<br />4）在 [回溯相容性設定向導] 中，按 **[下一步]**。<br />5）在 [程式維護] 頁面上，選取 [**修改**]，然後按 **[下一步]**。<br />6）在 [特徵選取] 頁面上，如果 [決策支援物件（DSO）] 無法使用，請按一下向下箭號，然後選取 [**此功能將會安裝在本機硬碟**]。 按 [下一步]  。<br />7）在 [準備修改程式] 頁面上，按一下 [**安裝**]。<br />8）當安裝完成時，按一下 **[完成]**。<br /><br /> <br /><br /> 您可以遵循先前的步驟，在完成遷移之後移除 DSO，將 DSO 的選項變更為「**此功能將無法使用**」。<br /><br /> 如果回溯相容性封裝未安裝，您可以從 SQL Server 2008 散發媒體加以安裝。 請注意，有適用於每一個目標架構 (x86、x64，ia64) 的版本。 這些版本可以從下列位置取得：<br /><br /> x86\Setup\x86\SQLServer2005_BC.msi<br /><br /> x64\Setup\x64\SQLServer2005_BC.msi<br /><br /> ia64\Setup\ia64\SQLServer2005_BC.msi|  
|建議您不要在 [資料] 資料夾中放置分割區位置。|伺服器會管理 [資料] 資料夾，並在建立、刪除和更改物件時，建立或卸除資料夾。 因此，強烈建議您不要在 [資料] 資料夾內指定分割區儲存體位置，特別是在資料庫、Cube 和維度的子資料夾中。 雖然伺服器可以讓您透過 Create 或 Alter 進行這項作業，但這麼做會顯示警告訊息。 當您將資料庫從 SQL Server 2005 Analysis Services 升級至在 [資料] 資料夾中具有分割區儲存體位置的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services 時，該作業會成功。 Restore 或 Sync 會要求您將分割區儲存體位置移到 [資料] 資料夾之外。|  
|如果是在 ProClarity Analytics Server 和 Microsoft Office PerformancePoint Server 2007 中使用 "EXISTING" MDX 關鍵字的查詢，則可能會獲得非預期的結果。|在特定的狀況下，ProClarity Analytics Server 和 Microsoft Office PerformancePoint Server 2007 會錯誤地使用 MDX 的 "EXISTING" 關鍵字。 由於 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services 中所做的變更之緣故，這些查詢可能會傳回非預期的結果。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Backward Compatibility](analysis-services-backward-compatibility.md)  
  
  
