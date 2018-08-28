---
title: Management Studio 中的自訂報表 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.summary.new.custom.report.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 1ba3f758-f39b-4f5f-91ca-516cedc78979
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71651e644d3547345a3e3c9b89637d3273e1f72e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42776586"
---
# <a name="custom-reports-in-management-studio"></a>Management Studio 中的自訂報表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，許多物件總管節點會顯示一組由 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 建立的標準報表。 這些報表會摘要列出經常要求的伺服器資訊。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 開始，管理員就可以從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] 執行在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中建立的自訂報表。  
  
## <a name="implementation"></a>實作  
自訂報表會儲存成報表定義 (.rdl) 檔案，而且這些檔案是使用報表定義語言 (RDL) 所建立的。 RDL 會包含 XML 格式之報表的資料擷取和配置資訊。 RDL 是一種開放式結構描述。 開發人員可以使用其他屬性和元素來擴充 RDL。 報表可以執行報表內的任何有效 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
如果 [物件總管] 連接至某部伺服器，而且自訂報表參考該節點的報表參數，則這些報表就可以在目前 [物件總管] 選取範圍的內容中執行。 這可讓報表使用目前的內容 (例如目前的資料庫) 或一致的內容 (例如將指派的資料庫指定為包含在自訂報表中之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的一部分)。  
  
## <a name="running-a-custom-report"></a>執行自訂報表  
您可以利用下列方式在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中執行自訂報表：  
  
-   以滑鼠右鍵按一下物件總管中的節點、指向 [報表]，然後以滑鼠左鍵按一下 [自訂報表]。 在 [開啟檔案] 對話方塊中，找出包含 .rdl 檔的資料夾，然後開啟適當的報表檔案。  
  
-   以滑鼠右鍵按一下物件總管中的節點、指向 [報表]、指向 [自訂報表]，然後從最近使用過的檔案清單中選取自訂報表。  
  
## <a name="limitations"></a>限制  
當您使用自訂報表時，請考量下列限制：  
  
-   為了防止意外執行惡意程式碼， [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 無法設定為自動執行報表，即使檔案系統設定為將 .rdl 檔與 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]產生關聯也一樣。 報表無法以程式設計方式在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中執行，而且無法透過 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]從命令列執行。  
  
-   您可以在未產生預期值的內容中執行自訂報表。 例如，您可以在未涉及複寫的資料庫內容中執行有關複寫的報表，也可以用無權存取產生正確報表所需之資訊的使用者身分來執行報表。 自訂報表的建立者會負責報表結構及其內容的有效性。  
  
-   您無法將自訂報表加入至標準報表的清單。  
  
-   報表所處理的程式碼可能會影響伺服器效能。  
  
-   自訂報表將無法支援子報表。  
  
-   報表中每個查詢的命令文字都不得透過運算式定義。  
  
-   命令 (查詢) 中所使用的任何查詢參數只能參考單一報表參數，而無法使用任何運算式運算子。  
  
-   報表命令 (查詢) 只支援「文字」和「預存程序」命令類型。  
  
-   報表架構不會提供任何逸出參數給查詢。 查詢作者必須確定其查詢不會遭受 SQL 資料隱碼攻擊。  
  
## <a name="managing-custom-reports"></a>管理自訂報表  
我們建議擁有許多自訂報表的使用者，最好使用具有適當 NTFS 檔案系統權限的檔案系統資料夾來組織這些報表。  
  
## <a name="permissions"></a>[權限]  
自訂報表會使用目前使用者的權限來執行。 若要防止惡意使用者變更報表所執行的查詢，包含報表檔案之檔案系統資料夾的權限應該要設定為限制存取。  
  
使用者以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務所使用的帳戶，都需要包含報表檔案之檔案系統資料夾的讀取權。  
  
雖然您可以在報表中內嵌任何有效的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 命令，但是此命令將不會執行。  
  
> [!CAUTION]  
> 您可以報表中內嵌任何有效 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，然後從報表中執行。 在高權限使用者帳戶底下執行報表可讓任何內嵌的指示執行，而不會受到挑戰。  
  

  
## <a name="see-also"></a>另請參閱  
[將自訂報表加入 Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[取消隱藏執行自訂報表警告](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[使用自訂報表搭配物件總管節點屬性](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
  
