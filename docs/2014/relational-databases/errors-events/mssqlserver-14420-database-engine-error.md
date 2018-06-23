---
title: MSSQLSERVER_14420 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 14420 (Database Engine error)
ms.assetid: 4a1d72b1-ab1b-4119-a11b-a8a05c6fdb45
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f9f5639ecd66fb67121586f78831478d7377e903
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037043"
---
# <a name="mssqlserver14420"></a>MSSQLSERVER_14420
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|14420|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum14420|  
|訊息文字|記錄傳送主要資料庫 %s.%s 的備份臨界值為 %d 分鐘，且已經有 %d 分鐘未執行備份記錄檔作業。 檢查代理程式記錄和記錄傳送監視器資訊。|  
  
## <a name="explanation"></a>說明  
 記錄傳送已經超過備份臨界值未執行同步處理。 備份臨界值是指產生警示之前，記錄傳送備份作業之間所能經歷的分鐘數。 此訊息不一定會指出記錄傳送發生問題。 不過，此訊息可能表示發生下列其中一個問題︰  
  
-   備份作業並未執行。 可能原因如下：主要伺服器執行個體上的 SQL Server Agent 服務未執行、作業已停用，或是作業的排程已變更。  
  
-   備份作業將失敗。 可能的原因如下：備份資料夾路徑無效、磁碟已滿，或是 BACKUP 陳述式可能失敗等任何其他原因。  
  
## <a name="user-action"></a>使用者動作  
 若要對此訊息進行疑難排解︰  
  
-   請確定主要伺服器執行個體正在執行 SQL Server Agent 服務，以及此主要資料庫的備份作業已啟用，並且已排程為根據適當的頻率執行。  
  
-   主要伺服器上的備份作業可能會失敗。 在此情況下，請檢查備份作業的作業記錄以找出原因。  
  
-   主要伺服器執行個體上執行的記錄傳送備份作業，可能無法連接到監視伺服器執行個體以更新 **log_shipping_monitor_primary** 資料表。 這可能是監視伺服器執行個體與主要伺服器執行個體之間的驗證問題所引起的。  
  
-   備份警示臨界值的值可能不正確。 最好至少將這個值設定為備份作業頻率的三倍。 如果您在設定並執行記錄傳送之後變更備份作業的頻率，則必須跟著更新備份警示臨界值的值。  
  
-   當監視伺服器執行個體離線之後又再次連線時，**log_shipping_monitor_primary** 資料表會在警示訊息作業執行之後才更新為最新的值。 若要以主要資料庫的最新資料更新監視資料表，請在主要伺服器執行個體上執行 **sp_refresh_log_shipping_monitor**。  
  
-   主要或監視伺服器執行個體上的日期或時間不正確。 這可能也會產生警示訊息。 可能是其中一個執行個體上的系統日期或時間經過修改所引起的。  
  
    > [!NOTE]  
    >  兩個伺服器執行個體上使用不同時區，應不致產生問題。  
  
## <a name="see-also"></a>另請參閱  
 [log_shipping_monitor_primary &#40;Transact SQL&#41;](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)   
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_help_log_shipping_monitor_primary &#40;Transact SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql)   
 [sp_refresh_log_shipping_monitor &#40;Transact SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)   
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
