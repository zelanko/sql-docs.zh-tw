---
title: 警示屬性-新增警示 （一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.general.f1
ms.assetid: f5c11610-62e3-44df-9800-a5dc35be4a09
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7103db4a681efadbf519dcb579a6587512577e33
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814934"
---
# <a name="alert-properties-new-alert-general-page"></a>警示屬性-新增警示 （一般頁面）
  使用此頁面即可檢視及修改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示的一般屬性。  
  
## <a name="options"></a>選項。  
 **名稱**  
 變更警示的名稱。  
  
 **啟用**  
 啟用警示。 若警示尚未啟用，警示中所指定的動作就不會發生。  
  
 **型別**  
 選取警示的類型：  
  
-   **SQL Server 事件警示** 會回應 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 事件記錄檔中的訊息。  
  
-   **SQL Server 效能條件警示** 會回應效能計數器中的特定條件。  
  
-   **WMI 事件警示** 會回應 Windows Management Instrumentation (WMI) 事件。  
  
## <a name="sql-server-event-alert-options"></a>SQL Server 事件警示選項  
 **資料庫名稱**  
 不論事件發生所在的資料庫為何，針對該事件指定一個資料庫或 **所有資料庫** ，來回應訊息。  
  
 **錯誤號碼**  
 指定此事件會回應錯誤，並指定錯誤號碼。  
  
 **Severity**  
 指定此事件會回應具特定嚴重性層級的任何訊息，並指定嚴重性層級。  
  
 **訊息包含下列內容時引發警示**  
 依特定字串來篩選事件。 若選取此選項，警示就只會回應包含特定字串的事件。  
  
 **訊息文字**  
 指定要用來篩選事件的字串。  
  
## <a name="sql-server-performance-condition-alerts"></a>SQL Server 效能條件警示  
 **物件**  
 指定要監視的效能物件。  
  
 **計數器**  
 指定要監視之效能物件內的計數器。  
  
 **執行個體**  
 指定要監視之計數器的執行個體。  
  
 **發出警示的時機為計數器達**  
 指定警示要回應的計數器行為。 例如，當 [Free space in tempdb (KB)] 計數器的值低於某個值時，您可能會希望警示針對如此的條件做出回應，或者當 [SQL Compilations/sec] 高於某個值時，您可能會希望警示針對如此的條件做出回應。  
  
 **Value**  
 指定計數器的值。  
  
## <a name="wmi-event-alert-options"></a>WMI 事件警示選項  
 **命名空間**  
 指定針對 WMI 查詢語言 (WQL) 陳述式使用的命名空間。 僅支援執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 之電腦上的命名空間。  
  
 **[資料集屬性]**  
 指定會識別警示所回應之事件的 WQL 陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [警示](alerts.md)   
 [伺服器事件的 WMI 提供者使用 WQL](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)   
 [使用錯誤號碼建立警示](create-an-alert-using-an-error-number.md)   
 [Create an Alert Using Severity Level](create-an-alert-using-severity-level.md)  
  
  
