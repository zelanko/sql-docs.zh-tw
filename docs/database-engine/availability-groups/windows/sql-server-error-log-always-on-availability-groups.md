---
title: SQL Server 錯誤記錄檔 (可用性群組)
description: 描述由 Always On 可用性群組回報的錯誤記錄檔事件。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
author: rothja
ms.author: jroth
ms.openlocfilehash: 81d31225838ec029a020af2df25753b26acd2fb1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75251255"
---
# <a name="sql-server-error-log-always-on-availability-groups"></a>SQL Server 錯誤記錄檔 (Always On 可用性群組)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server 錯誤記錄檔報告影響 Always On 可用性群組的事件，如：  
  
-   與 Windows Server 容錯移轉叢集 (WSFC) 叢集的通訊    
-   可用性複本的狀態轉換    
-   可用性資料庫的狀態轉換    
-   主要與次要複本之間的可用性資料庫連線能力狀態    
-   可用性群組端點的狀態    
-   可用性群組接聽程式的狀態    
-   SQL Server 資源 DLL (在 WSFC 叢集中執行) 和 SQL Server 執行個體之間的租用狀態 (如需詳細資訊，請參閱[運作方式：SQL Server Always On 租用逾時](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx) \(英文\))    
-   可用性群組中的錯誤事件  

下列徵兆應該需要檢閱 SQL Server 錯誤記錄檔：  

-   無法存取可用性資料庫    
-   非預期的可用性群組容錯移轉    
-   可用性群組意外地處於 [正在解決] 狀態    
-   處於不定狀態的可用性群組  
  
如需詳細資訊，請參閱[檢視 SQL Server 錯誤記錄檔 &#40;SQL Server Management Studio&#41;](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)。  
  
  
