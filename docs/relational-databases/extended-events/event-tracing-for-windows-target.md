---
title: Windows 事件追蹤目標 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- event tracing for windows target
- ETW target
- targets [SQL Server extended events], event tracing for windows target
ms.assetid: ca2bb295-b7f6-49c3-91ed-0ad4c39f89d5
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac1191d870d7fe745cdbed0e17892c5c2cf34435
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021857"
---
# <a name="event-tracing-for-windows-target"></a>Windows 事件追蹤目標

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  使用 Windows 事件追蹤 (ETW) 當做目標之前，我們建議您最好具備 ETW 的實用知識。 ETW 追蹤會搭配擴充事件一起使用，或是當做擴充事件的事件取用者使用。 下列外部連結提供取得有關 ETW 之背景資訊的起點：  
  
-   [Windows 事件](https://go.microsoft.com/fwlink/?LinkId=92380)  
  
-   [使用 ETW 改善偵錯和效能調整](https://go.microsoft.com/fwlink/?LinkId=92381)  
  
 ETW 目標是單一目標，但是此目標可加入至許多工作階段。 如果某個事件在許多工作階段上引發，只會在每次發生事件時，將該事件傳播至 ETW 目標一次。 在每一個處理序上，擴充事件引擎則限制為單一執行個體。  
  
> [!IMPORTANT]  
>  為了讓 ETW 目標運作， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶必須是 Performance Log Users 群組的成員。  
  
 ETW 工作階段中的事件組態是由裝載擴充事件引擎的處理序所控制。 此引擎會控制要引發的事件以及讓事件發生所必須符合的條件。  
  
 當繫結至擴充事件工作階段之後 (在處理序存留期間第一次附加 ETW 目標)，ETW 目標會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者上開啟單一 ETW 工作階段。 如果 ETW 工作階段已經存在，ETW 目標會取得現有工作階段的參考。 這個 ETW 工作階段可在給定電腦上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間共用， 這個 ETW 工作階段會從具有 ETW 目標的工作階段中接收所有事件。  
  
 因為 ETW 需要啟用提供者，才能取用事件並將事件往下流向 ETW，所以會在此工作階段上啟用所有擴充的事件封裝。 當引發事件時，ETW 目標會傳送此事件到工作階段 (此工作階段上已啟用此事件的提供者)。  
  
 ETW 目標支援在引發事件的執行緒上同步發行事件。 不過，ETW 目標不支援非同步的事件發行。  
  
 ETW 目標不支援來自外部 ETW 控制器的控制，例如 Logman.exe。 若要產生 ETW 追蹤，您必須使用 ETW 目標來建立事件工作階段。 如需詳細資訊，請參閱 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)。  
  
> [!NOTE]  
>  啟用 ETW 目標就會建立名為 XE_DEFAULT_ETW_SESSION 的 ETW 工作階段。 如果具有 XE_DEFAULT_ETW_SESSION 名稱的工作階段已經存在，就會使用此工作階段，而不修改現有工作階段的任何屬性。 XE_DEFAULT_ETW_SESSION 會在所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之間共用。 啟動 XE_DEFAULT_ETW_SESSION 之後，您必須使用 Logman 工具等 ETW 控制器來停止它。 例如，您可以在命令提示字元中執行下列命令： **logman stop XE_DEFAULT_ETW_SESSION -ets**。  
  
 下表描述用於設定 ETW 目標的可用選項。  
  
|選項|允許的值|Description|  
|------------|--------------------|-----------------|  
|default_xe_session_name|最多 256 個字元的任何字串。 此為選擇性的值。|擴充事件工作階段名稱。 根據預設，這個名稱是 XE_DEFAULT_ETW_SESSION。|  
|default_etw_session_logfile_path|最多 256 個字元的任何字串。 此為選擇性的值。|擴充事件工作階段之記錄檔的路徑。 根據預設，這個路徑是 %TEMP%\ XEEtw.etl。|  
|default_etw_session_logfile_size_mb|任何不帶正負號的整數。 此為選擇性的值。|擴充事件工作階段的記錄檔案大小 (以 MB 為單位)。 預設值是 20 MB。|  
|default_etw_session_buffer_size_kb|任何不帶正負號的整數。 此為選擇性的值。|擴充事件工作階段的記憶體中緩衝區大小 (以 KB 為單位)。 預設值是 128 KB。|  
|重試次數|任何不帶正負號的整數。|在卸除事件之前，重試將此事件發行給 ETW 子系統的次數。 預設值是 0。|  
| &nbsp; | &nbsp; | &nbsp; |

 這些設定都是選擇性的。 ETW 目標會使用這些設定的預設值。  
  
 ETW 目標負責以下工作：  
  
-   建立預設 ETW 工作階段。  
  
-   將所有擴充的事件封裝向 ETW 註冊。 如此可確保 ETW 不會卸除事件。  
  
-   管理對 ETW 的事件流程。 ETW 目標會以擴充的事件資料來建立 ETW 事件，然後將它傳送給適當的 ETW 工作階段。 如果此事件大於緩衝區大小，或是資料無法納入一個 ETW 事件中，則 ETW 會將此事件分割若干片段。  
  
-   請隨時將擴充的事件封裝保持在啟用狀態。  
  
 下列的預設檔案位置是由 ETW 所使用：  
  
-   ETW 輸出檔位於 %TEMP%\XEEtw.etl 中。  
  
    > [!IMPORTANT]  
    >  當第一個工作階段啟動之後，將無法變更檔案路徑。  
  
-   受管理物件格式 (MOF) 檔案位於 *\<安裝路徑>* \Microsoft SQL Server\Shared 中。 如需詳細資訊，請參閱 MSDN 上的 [Managed Object Format (MOF)](https://go.microsoft.com/fwlink/?LinkId=92851) (管理物件格式)。

<!-- ?LinkId=92851  ==  https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-
-->

## <a name="adding-the-target-to-a-session"></a>將目標加入至工作階段  
 若要將 ETW 目標加入至擴充事件工作階段，您必須在建立或改變事件工作階段時，加入下列陳述式：  
  
```sql
ADD TARGET package0.etw_classic_sync_target  
```  
  
 如需示範如何使用 ETW 目標 (包括如何檢視資料) 之完整範例的詳細資訊，請參閱 [使用擴充事件監視系統活動](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 擴充的事件目標](targets-for-extended-events-in-sql-server.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)  
  
  
