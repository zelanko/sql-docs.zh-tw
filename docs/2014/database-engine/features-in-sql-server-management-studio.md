---
title: SQL Server Management Studio 中的功能 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], about SQL Server Management Studio
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: e75504b9-7968-4e3b-8411-fd79fe09021e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: bd2d11c35f46d3cd60cb2180eca40fe45f41105a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933039"
---
# <a name="features-in-sql-server-management-studio"></a>SQL Server Management Studio 中的功能
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 包括下列一般功能：  
  
-   支援 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的大部分管理工作。  
  
-   用來管理和撰寫 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的單一整合式環境。  
  
-   用來管理 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中之物件的對話方塊，可讓您立即執行動作、將它們傳給程式碼編輯器，或編寫它們的指令碼，以便稍後執行。  
  
-   非強制回應和可調整大小的對話，允許當對話在開啟狀態時，存取多個工具。  
  
-   一般排程對話，可讓您稍後再執行管理對話的動作。  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 環境之間，匯出和匯入 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 伺服器註冊。  
  
-   儲存或列印 SQL Server Profiler 所產生的 XML 執行程序表或死結檔案，以便稍後檢視它們，或將它們傳給管理員來進行分析。  
  
-   提供更多資訊的新錯誤和參考訊息方塊，可讓您將訊息的相關註解傳給 [!INCLUDE[msCoName](../includes/msconame-md.md)] 、將訊息複製到剪貼簿，以及輕易地利用電子郵件將訊息傳給支援團隊。  
  
-   用來快速瀏覽 MSDN 或線上說明的整合式 Web 瀏覽器。  
  
-   線上社群的說明整合。  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的教學課程，可協助您使用許多新功能，當下提升您的生產力。  
  
-   能夠進行篩選和自動重新整理的新活動監視器。  
  
-   整合式 Database Mail 介面。  
  
## <a name="new-scripting-capabilities"></a>新增指令碼功能  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的程式碼編輯器元件包含用來撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)]、MDX、DMX 和 XML/A 指令碼的整合式指令碼編輯器。 它的功能如下：  
  
-   在工作時即時存取相關資訊的動態說明。  
  
-   一組非常豐富的範本，且能夠建立自訂範本。  
  
-   支援不需要連接到伺服器，就能夠撰寫和編輯查詢或指令碼。  
  
-   SQLCMD 查詢和指令碼的指令碼編寫支援。  
  
-   用來檢視 XML 結果的新介面。  
  
-   方案和指令碼專案的整合式原始檔控制，支援儲存和維護隨著時間而進展的指令碼副本。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] MDX 陳述式的 IntelliSense 支援。  
  
## <a name="object-explorer-features"></a>物件總管功能  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的物件總管元件是用來檢視和管理所有伺服器類型之物件的整合式工具。 它的功能如下：  
  
-   依名稱、結構描述或日期的全部或一部分來篩選。  
  
-   進行物件的非同步擴展，且能夠根據中繼資料來篩選物件。  
  
-   存取複寫伺服器中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent，以進行管理。  
  
 如需詳細資訊，請參閱 [物件總管](../ssms/object/object-explorer.md)。  
  
## <a name="extensibility"></a>擴充性  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 會根據 Visual Studio 隔離 Shell 來建構，該隔離 Shell 原本就支援擴充性 (增益集/外掛程式)。 挖掘 Visual Studio 擴充性服務來呈現 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]內的自訂功能是可行的，但是這樣的擴充性不受支援。  
  
 有些使用者和協力廠商已開發 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的延伸模組。 雖然我們不阻止這樣做，但請記住，我們不支援這類擴充性，因此可能會有向後/向前相容性問題。 Microsoft 不會發行擴充 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的文件。 不過，確實社群部落格和範例程式碼，您可以加以運用。  
  
 Microsoft 不支援已存在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 延伸模組的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 安裝，所以如果您已安裝 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 延伸模組，您可能會想要先加以移除，然後再撥打電話給 Microsoft 客戶支援服務來解決 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 問題。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)  
  
  
