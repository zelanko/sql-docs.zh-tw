---
title: "DQS 安全性 | Microsoft Docs"
ms.custom: 
ms.date: 10/01/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 921927f5-1b1e-452a-a79e-c691829fd826
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 645ef08b3abe78411236d0101d2ee8a9be7cc1f2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="dqs-security"></a>DQS 安全性
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 安全性基礎結構是根據 SQL Server 安全性基礎結構。 資料庫管理員會將使用者與 DQS 角色產生關聯，將一組權限授與該使用者。 這樣做會決定使用者可存取的 DQS 資源以及允許使用者執行的功能活動。  
  
## <a name="dqs-roles"></a>DQS 角色  
 DQS 有四個角色。 其中一個是資料庫管理員 (DBA)，他主要負責處理產品安裝、資料庫維護和使用者管理。 這個角色主要是使用 SQL Server Management Studio，而不是 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式。 其伺服器角色是系統管理員 (sysadmin)。  
  
 還有兩個其他角色，分別是資訊工作者，以及在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式中工作來直接使用產品的資料監管。 這些角色包括下列各項：  
  
-   **DQS 系統管理員** (dqs_administrator 角色) 可以在產品的範圍內執行任何工作。 管理員可以編輯和執行專案、建立和編輯知識庫、終止活動、停止活動內的程序，也可以變更組態和參考資料服務設定。 但是 DQS 管理員無法安裝伺服器或新增使用者。 這必須由資料庫管理員來執行。  
  
-   **DQS KB 編輯者** (dqs_kb_editor 角色) 可以執行管理以外的所有 DQS 活動。 KB 編輯者可以編輯和執行專案以及建立和編輯知識庫。 他們可以看到活動監控資料，但不能終止或停止活動或是履行管理職責。  
  
-   **DQS KB 操作員** (dqs_kb_operator 角色) 可以編輯和執行專案。 他們不能執行任何種類的知識管理，也不能建立或變更知識庫。 他們可以看到活動監控資料，但不能終止活動或履行管理職責。  
  
## <a name="user-management"></a>使用者管理  
 資料庫管理員 (DBA) 會建立 DQS 使用者，並在 SQL Server Management Studio 中將這些使用者與 DQS 角色產生關聯。 DBA 會管理其權限，方法是新增 SQL 登入當做 DQS_MAIN 資料庫的使用者，並將每一個使用者與其中一個 DQS 角色產生關聯。 每個角色都會被授與 DQS_MAIN 資料庫上一組預存程序的權限。 這三個 DQS 角色不適用於 DQS_PROJECTS 和 DQS_STAGING_DATA 資料庫。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何使用 SQL Server Management Studio 建立使用者及授與 DQS 角色。|[在 SSMS 中管理 DQS 使用者](http://msdn.microsoft.com/library/955af01d-00da-4c51-9311-f3848749df54)|  
  
  
