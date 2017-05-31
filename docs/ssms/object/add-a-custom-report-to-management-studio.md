---
title: "將自訂報表加入 Management Studio | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 3cf8d726-0a90-4f80-98d0-352a2a59be0f
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 04726d3d8f01dbb667ab728abd56fce8e7ce3933
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="add-a-custom-report-to-management-studio"></a>將自訂報表加入 Management Studio
本主題描述如何建立儲存為 .rdl 檔案的簡單 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] 報表，然後將該 rdl 檔案加入至 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 做為自訂報表。 [!INCLUDE[ssRS](../../includes/ssrs_md.md)] 可以建立多種精密報表。 若要使用本主題來建立報表，您必須先在電腦上安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] 。 您不需要在 [!INCLUDE[ssRS](../../includes/ssrs_md.md)] 上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ，即可使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]執行自訂報表。  
  
 
### <a name="to-create-a-simple-report-saved-as-an-rdl-file"></a>建立儲存成 .rdl 檔的簡單報表  
  
1.  按一下 [開始]、依序指向 [程式集] 和 [Microsoft SQL Server]，然後按一下 [SQL Server Data Tools]。  
  
2.  在 **[檔案]** 功能表上，指向 **[開新檔案]**，然後按一下 **[專案]**。  
  
3.  在 **[專案類型]** 清單中，按一下 **[商業智慧專案]**。  
  
4.  在 [範本] 清單中，按一下 [報表伺服器專案精靈]。  
  
5.  在 [名稱] 中，輸入 **ConnectionsReport**，然後按一下 [確定]。  
  
6.  在 [報表精靈] 簡介頁面中，按一下 [下一步]。  
  
7.  在 [選取資料來源] 頁面的 [名稱] 方塊中，為 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 的這個連接輸入名稱，然後按一下 [編輯]。  
  
8.  在 [連接屬性] 對話方塊的 [伺服器名稱] 方塊中，輸入您的 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 執行個體名稱。  
  
9. 在 [請選取或輸入資料庫名稱] 方塊中，輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 上任何資料庫的名稱 (例如 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)])，然後按一下 [確定]。  
  
10. 在 [選取資料來源] 頁面上，按一下 [下一步]。  
  
11. 在 [設計查詢] 頁面的 [查詢字串] 方塊中，輸入下列 [!INCLUDE[tsql](../../includes/tsql_md.md)] 陳述式 (可列出 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 的目前連接)，然後按一下 [下一步]。 [報表精靈] 的 [查詢字串] 方塊無法接受報表參數。 您必須手動建立更複雜的自訂報表。  
  
    **SELECT session_id, net_transport FROM sys.dm_exec_connections;**  
  
12. 在 [選取報表類型] 頁面上，選取 [表格式]，然後按一下 [完成]。  
  
13. 在 [正在完成精靈] 頁面的 [報表名稱] 方塊中，輸入 **ConnectionsReport**，然後按一下 [完成] 建立並儲存報表。  
  
14. 關閉 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio_md.md)]。  
  
15. 將 **ConnectionsReport.rdl** 複製到您在資料庫伺服器上針對自訂報表所建立資料夾。  
  
### <a name="to-add-a-report-to-management-studio"></a>將報表加入至 Management Studio  
  
-   在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 中，以滑鼠右鍵按一下物件總管中的節點、指向 [報表]，然後按一下 [自訂報表]。 在 [開啟檔案] 對話方塊中，找到自訂報表資料夾，並選取 **ConnectionsReport.rdl** 檔案，然後按一下 [開啟]。  
  
    第一次從物件總管節點開啟新的自訂報表時，此自訂報表就會新增至該節點快速鍵功能表上 [自訂報表] 底下的最近使用清單。 第一次開啟標準報表時，該報表也會顯示在 [自訂報表] 下之最近使用的清單中。 如果您刪除了某個自訂報表檔，下次選取該項目時，系統就會提示您是否要從最近使用清單中刪除該項目。  
  
    1.  若要變更最近使用清單中可顯示的檔案數目，請在 [工具] 功能表中，按一下 [選項]、展開 [環境] 資料夾，然後按一下 [一般]。  
  
    2.  調整 [顯示最近使用清單中的檔案] 的數目。  
  
## <a name="see-also"></a>另請參閱  
[Management Studio 中的自訂報表](../../ssms/object/custom-reports-in-management-studio.md)  
[使用自訂報表搭配物件總管節點屬性](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
[取消隱藏執行自訂報表警告](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[SQL Server Reporting Services](http://msdn.microsoft.com/en-us/b8d18d3d-9db0-43e7-8286-7b46cc3a37ed)  
  

