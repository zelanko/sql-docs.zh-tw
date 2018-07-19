---
title: MSSQLSERVER_14421 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 14421 (Database Engine error)
ms.assetid: 03e76d4a-d463-4673-8843-08e4ecaefe27
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 29efb64c800d74a2e9c88db06d40c55a229d731d
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415557"
---
# <a name="mssqlserver14421"></a>MSSQLSERVER_14421
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|14421|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum14421|  
|訊息文字|記錄傳送次要資料庫 %s.%s 的還原臨界值為 %d 分鐘，而且未同步。已經有 %d 分鐘未執行還原。 還原的延遲為 %d 分鐘。 檢查代理程式記錄和記錄傳送監視器資訊。|  
  
## <a name="explanation"></a>說明  
 此訊息表示記錄傳送未同步，而且超過還原臨界值。 還原臨界值是指產生訊息之前，還原作業之間經歷的分鐘數。  
  
### <a name="possible-causes"></a>可能的原因  
 此訊息不一定會指出記錄傳送發生問題。 不過，此訊息可能表示發生下列其中一個問題︰  
  
-   還原作業並未執行。  
  
     作業未執行的可能原因如下︰次要伺服器執行個體上的 SQL Server Agent 服務未執行、作業已停用，或是作業的排程已變更。  
  
-   還原作業將失敗。  
  
     作業失敗的可能原因如下︰還原資料夾路徑無效、磁碟已滿，或是 RESTORE 陳述式可能失敗等任何其他原因。  
  
## <a name="user-action"></a>使用者動作  
 若要對此訊息進行疑難排解︰  
  
-   請確定次要伺服器執行個體正在執行 SQL Server Agent 服務、此次要資料庫的還原作業已啟用，並且會依照排程以適當的頻率執行。  
  
-   次要伺服器上的還原作業可能會失敗。 在此情況下，請檢查還原作業的作業記錄以找出原因。  
  
-   次要伺服器執行個體上執行的記錄傳送還原作業，可能無法連接到監視伺服器執行個體以更新 **log_shipping_monitor_secondary** 資料表。 這可能是監視伺服器執行個體與次要伺服器執行個體之間的驗證問題所引起的。  
  
-   備份警示臨界值的值可能不正確。 這個值最好是設定為還原作業頻率的三倍以上。 如果您在設定並執行記錄傳送之後變更還原作業的頻率，則必須跟著更新備份警示臨界值的值。  
  
-   當監視伺服器執行個體離線之後又再度連線時，**log_shipping_monitor_secondary** 資料表會在警示訊息作業執行之後才更新為最新的值。 若還原作業成功但顯示「找不到可套用至次要資料庫的記錄備份檔案」，可能會發生錯誤 14421。 發生此錯誤時，還原時間便不會更新。 這個情況的錯誤原因可能是複製作業發生問題。  
  
     若要以次要資料庫的最新資料更新監視資料表，請在次要伺服器執行個體上執行 **sp_refresh_log_shipping_monitor**。  
  
-   次要或監視伺服器執行個體上的日期或時間不正確。 這可能也會產生警示訊息。 可能是其中一個執行個體上的系統日期或時間經過修改所引起的。  
  
    > [!NOTE]  
    >  兩個伺服器執行個體上使用不同時區，應不致產生問題。  
  
## <a name="see-also"></a>另請參閱  
 [log_shipping_monitor_secondary &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)   
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_help_log_shipping_monitor_secondary &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql)   
 [sp_refresh_log_shipping_monitor &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)   
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
