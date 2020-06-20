---
title: 記錄檔檢視器 F1 說明 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configurelogs.errorlog.f1
helpviewer_keywords:
- Log File Viewer
ms.assetid: 2243845c-4880-4aa0-9ee8-0a97a128996b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c6eadb4baa4a47202b40a9cde1eca896022f31d7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049790"
---
# <a name="log-file-viewer-f1-help"></a>記錄檔檢視器 F1 說明
  記錄檔檢視器會顯示許多不同元件的記錄資訊。 當記錄檔檢視器開啟時，使用 **[選取記錄]** 窗格以選取您要顯示的記錄檔。 每個記錄檔都會顯示適用於該記錄檔類型的資料行。  
  
 可用的記錄檔取決於記錄檔檢視器的開啟方式而定。 如需詳細資訊，請參閱 [開啟記錄檔檢視器](open-log-file-viewer.md)。  
  
 您可以在 [工具/選項]  對話方塊的 [SQL Server 物件總管/命令]  頁面中，設定要顯示的稽核記錄檔資料列數目。 如需稽核記錄檔顯示之資料行的描述，請參閱 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)。  
  
## <a name="options"></a>選項。  
 **載入記錄**  
 開啟對話方塊供您指定所要載入的記錄檔。  
  
 **匯出**  
 開啟對話方塊，以讓您將 [記錄檔摘要]  格線中所顯示的資訊匯出至文字檔。  
  
 **[重新整理]**  
 重新整理所選取之記錄檔的檢視。 當套用任何篩選設定時， **[重新整理]** 按鈕會從目標伺服器重新讀取選取的記錄檔。  
  
 **Filter**  
 開啟對話方塊，以讓您指定用來篩選記錄檔的設定，例如 [連接]  、[日期]  或其他的 [一般]  篩選準則。  
  
 **搜尋**  
 搜尋記錄檔中的特定文字。 不支援使用萬用字元搜尋。  
  
 **停止**  
 停止載入記錄檔項目。 例如，如果遠端或離線記錄檔需要長時間才能載入，而您只要檢視最新項目時，就可以使用這個選項。  
  
 **記錄檔摘要**  
 此資訊面板會顯示記錄檔篩選的摘要。 如果未篩選檔案，則會看到下列文字： **[未套用篩選]** 。 若篩選已套用到記錄，則會看到下列文字：**篩選記錄項目的準則：** \<filter criteria>。  
  
 **選取的資料列詳細資料**  
 選取資料列以顯示頁面下方有關選取之事件資料列的其他詳細資料。 將資料行拖曳至方格中的新位置，以重新排序資料行。 將方格標頭中的資料行分隔線拖曳至左邊或右邊，以調整資料行大小。 在方格標頭中按兩下資料行分隔線，自動將資料行大小調整為內容寬度。  
  
 **執行個體**  
 發生事件之執行個體的名稱。 顯示為 *&lt;電腦名稱*\\*執行個體名稱&gt;* 。  
  
## <a name="frequently-displayed-columns"></a>經常顯示的資料行  
 **日期**  
 顯示事件的日期。  
  
 **Source**  
 顯示事件建立的來源功能，例如服務名稱 (如 MSSQLSERVER)。 不是所有記錄檔類型都會出現來源。  
  
 **訊息**  
 顯示與事件相關聯的任何訊息。  
  
 **記錄類型**  
 顯示事件所屬之記錄檔的類型。 所有選取的記錄檔都會出現在記錄檔摘要視窗中。  
  
 **記錄來源**  
 顯示擷取事件之來源記錄的描述。  
  
## <a name="permissions"></a>權限  
 若要存取線上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的記錄檔，需要 securityadmin 固定伺服器角色的成員資格。  
  
 若要存取離線 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的記錄檔，您必須具有 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空間以及儲存記錄檔之資料夾的讀取權限。 如需詳細資訊，請參閱 [檢視離線記錄檔](view-offline-log-files.md)主題中的＜安全性＞一節。  
  
## <a name="see-also"></a>另請參閱  
 [記錄檔檢視器](log-file-viewer.md)   
 [開啟記錄檔檢視器](open-log-file-viewer.md)   
 [檢視離線記錄檔](view-offline-log-files.md)  
  
  
