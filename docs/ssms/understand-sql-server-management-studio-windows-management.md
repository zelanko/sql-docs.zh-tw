---
title: "了解 SQL Server Management Studio 視窗管理 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- autohide [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], tool windows
- push pin [SQL Server Management Studio]
- tool windows [SQL Server Management Studio]
ms.assetid: bebf8383-dcaf-466e-84f5-63b81c9cfe52
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 509fcf51c1f3caadad4068ba564c6cf91119878c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="understand-sql-server-management-studio-windows-management"></a>了解 SQL Server Management Studio 視窗管理
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 中的工具視窗是機能性、靈活性和有效性都非常高的系統，可讓您執行下列動作：  
  
-   將使用者用來進行開發或管理的工作空間最大化。  
  
-   減少同時顯示的未用視窗數目。  
  
-   容易自訂使用者環境。  
  
視窗的操作是 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 環境的核心工作。 使用者很容易存取他們常用的工具和視窗。 使用者可以控制他們要配置給不同資訊的空間量，環境應該據此將編輯查詢所能使用的空間最大化。 視窗可以移至螢幕的不同位置。 您可以使許多視窗成為非固定，以及將它們拖出 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 框架。 當使用多個監視器時，這尤其有用。  
  
為了既能維護功能，又增加編輯空間，所有視窗都提供了「自動隱藏」功能，它會將視窗顯示成沿著主要 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 環境的框線而出現的一列之內的索引標籤。 當指標停在這些索引標籤的其中一個標籤上時，下面的視窗便會浮現出。 您可以按一下 [自動隱藏] 按鈕來切換視窗的「自動隱藏」功能，這個按鈕就是視窗右上角的圖釘。 另外，[視窗] 功能表也有 [自動全部隱藏] 選項。  
  
您可以在索引標籤模式或多重文件介面 (MDI) 模式中設定某些元件。在索引標籤模式中，多個元件會顯示成在同一個固定位置的索引標籤；在多重文件介面 (MDI) 模式中，每份文件都有它自己的視窗。 若要設定這項功能，請在 [工具] 功能表上，按一下 [選項] 和 [環境]，再按一下 [一般]。  
  
> [!IMPORTANT]  
> 當登入 (或自主資料庫使用者) 連接並通過驗證時，此連接就會儲存有關登入的識別資訊。 若為 Windows 驗證登入，這就包括 Windows 群組中成員資格的相關資訊。 只要維持連接，登入的識別就會維持驗證狀態。 若要強制變更識別 (例如重設密碼或變更 Windows 群組成員資格)，登入必須先登出驗證授權單位 (Windows 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)])，然後重新登入。 **系統管理員 (sysadmin)** 固定伺服器角色的成員或任何擁有 **ALTER ANY CONNECTION** 權限的登入都可以使用 **KILL** 命令來結束連接並強制登入重新連接。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 可以在開啟 [物件總管] 視窗和 [查詢編輯器] 視窗的多個連接時，重複使用連接資訊。 關閉所有連接以強制重新連接。  
  
> [!IMPORTANT]  
> 當登入 (或自主資料庫使用者) 連接並通過驗證時，此連接就會快取有關登入的識別資訊。 若為 Windows 驗證登入，這就包括 Windows 群組中成員資格的相關資訊。 只要維持連接，登入的識別就會維持驗證狀態。 若要強制變更識別 (例如重設密碼或變更 Windows 群組成員資格)，登入必須先登出驗證授權單位 (Windows 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)])，然後重新登入。 **系統管理員 (sysadmin)** 固定伺服器角色的成員或任何擁有 **ALTER ANY CONNECTION** 權限的登入都可以使用 **KILL** 命令來結束連接並強制登入重新連接。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 可以在開啟 [物件總管] 視窗和 [查詢編輯器] 視窗的多個連接時，重複使用連接資訊。 關閉所有連接以強制重新連接。  
  
## <a name="see-also"></a>另請參閱  
[使用 SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[SQL Server Management Studio 環境](../ssms/the-sql-server-management-studio-environment.md)  
  
