---
title: SQL Server 錯誤記錄檔 (可用性群組)
description: 了解影響 Always On 可用性群組的 SQL Server 錯誤記錄檔事件，以及哪些徵兆應該需要檢閱錯誤記錄檔。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
author: rothja
ms.author: jroth
ms.openlocfilehash: b33827f37d02edf783c4688c9ad08cd4673706e7
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670881"
---
# <a name="sql-server-error-log-always-on-availability-groups"></a>SQL Server 錯誤記錄檔 (Always On 可用性群組)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  SQL Server 錯誤記錄檔報告影響 Always On 可用性群組的事件，如：  
  
-   與 Windows Server 容錯移轉叢集 (WSFC) 叢集的通訊    
-   可用性複本的狀態轉換    
-   可用性資料庫的狀態轉換    
-   主要與次要複本之間的可用性資料庫連線能力狀態    
-   可用性群組端點的狀態    
-   可用性群組接聽程式的狀態    
-   SQL Server 資源 DLL (在 WSFC 叢集中執行) 和 SQL Server 執行個體之間的租用狀態 (如需詳細資訊，請參閱 [How It Works:SQL Server Always On Lease Timeout](/archive/blogs/psssql/how-it-works-sql-server-alwayson-lease-timeout)) (運作方式：SQL Server Always On 租用逾時)    
-   可用性群組中的錯誤事件  

下列徵兆應該需要檢閱 SQL Server 錯誤記錄檔：  

-   無法存取可用性資料庫    
-   非預期的可用性群組容錯移轉    
-   可用性群組意外地處於 [正在解決] 狀態    
-   處於不定狀態的可用性群組  
  
如需詳細資訊，請參閱[檢視 SQL Server 錯誤記錄檔 &#40;SQL Server Management Studio&#41;](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)。  
  
