---
title: 維護計畫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- SQL12.AG.MAINTPLAN.LEGACY.F1
helpviewer_keywords:
- maintenance plans [SQL Server], about database maintenance plans
- maintenance plans [SQL Server], database compatibility level displayed in designer
- maintenance plans [SQL Server]
ms.assetid: 5982ca65-74fe-44e3-aef9-00a65a0db169
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0643c6fbf8e9a6aa649d4d335117bcb4f5b35208
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52803070"
---
# <a name="maintenance-plans"></a>維護計畫
  維護計畫會建立必要的工作流程，確保資料庫已最佳化、定期備份，而且沒有任何不一致性。 「維護計畫精靈」也會建立核心維護計畫，但手動建立計畫能提供更大的彈性。  
  
## <a name="benefits-of-maintenance-plans"></a>維護計畫的優點  
 在 [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)] 中，維護計畫會建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，再由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業執行。 維護計畫可以依排程間隔手動或自動執行。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 維護計畫提供下列功能：  
  
-   使用各種典型的維護工作來建立工作流程。 您也可以建立您自己的自訂 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。  
  
-   概念階層。 每項計畫都可以讓您建立或編輯工作流程。 每項計畫中的工作可以再分為子計畫，然後排定在不同時間執行。  
  
-   支援多伺服器計畫，可用於主要伺服器/目標伺服器環境。  
  
-   支援記錄計畫記錄到遠端伺服器。  
  
-   支援 Windows 驗證和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="maintenace-plan-functionality"></a>維護計畫功能  
 您可以建立維護計畫來執行下列工作：  
  
-   以新的填滿因數重建索引，重新整理資料以及索引頁上的資料。 使用新的填滿因數重建索引時，可以確保資料庫頁面包含平均分佈的資料量和可用空間。 也可以在未來快速擴展。 如需詳細資訊，請參閱[指定索引的填滿因素](../indexes/specify-fill-factor-for-an-index.md)。  
  
-   藉由移除空的資料庫頁面來壓縮資料檔案。  
  
-   更新索引統計資料，以確保查詢最佳化工具對於資料表中的資料值分佈，擁有最新的資訊。 由於查詢最佳化工具對資料庫儲存的資料已掌握詳細資訊，因此可以更準確地判斷存取資料的最佳方式。 雖然 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會定期自動更新索引統計資料，但此選項可以強制統計資料立即更新。  
  
-   對資料庫內的資料及資料頁執行內部一致性檢查，確保系統或軟體問題未損毀資料。  
  
-   備份資料庫及交易記錄檔。 資料庫及記錄備份可以保留至特定的時間。 這樣可讓您建立備份的記錄，當您需要將資料庫還原到比上一次資料庫備份更早之前的時間，即可使用此一記錄。 您也可以執行差異備份。  
  
-   執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。 這可用來建立執行各種動作的作業，以及執行這些作業的維護計畫。  
  
 維護工作產生的結果可以當做報表寫入文字檔，或寫入 `sysmaintplan_log` 中的維護計畫資料表 `sysmaintplan_logdetail` 和 `msdb`。 若要在記錄檔檢視器中檢視結果，請以滑鼠右鍵按一下 [維護計畫]，然後按一下 [檢視記錄]。  
  
## <a name="related-tasks"></a>相關工作  
 若要開始使用維護計畫，請使用下列主題。  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建立維護計畫。|[建立維護計畫](create-a-maintenance-plan.md)|  
|描述如何使用維護計畫設計介面建立維護計畫。|[建立維護計畫 &#40;維護計畫設計介面&#41;](create-a-maintenance-plan-maintenance-plan-design-surface.md)|  
|記載 [物件總管] 中可用的維護計畫功能。|[維護計畫節點 &#40;物件總管&#41;](../../ssms/object/object-explorer.md)|  
  
  
