---
title: 在物件總管中管理事件工作階段 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 16849e38-d3fb-414d-8dcb-797b5ffce6ee
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 70b2160c9ecaab75670ae1088c556745ed289967
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/26/2019
ms.locfileid: "58477993"
---
# <a name="manage-event-sessions-in-the-object-explorer"></a>在物件總管中管理事件工作階段

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  本主題將討論您可以在 **[物件總管]** 中採取以影響「擴充事件」的動作：  
  
-   建立擴充事件工作階段  
  
-   啟動或停止擴充事件工作階段  
  
-   匯出擴充事件工作階段  
  
-   匯入擴充事件工作階段範本  
  
-   編輯擴充事件工作階段  
  
-   刪除擴充事件工作階段  
  
## <a name="create-an-extended-events-session"></a>建立擴充事件工作階段  
 如需有關建立「擴充事件」工作階段的詳細資訊，請參閱＜ [Create an Extended Events Session](https://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)＞。  
  
## <a name="starting-or-stopping-an-extended-events-session"></a>啟動或停止擴充事件工作階段  
 您可以透過 **[查詢編輯器]** (使用 **ALTER EVENT SESSION** 陳述式) 或使用 **[物件總管]** 的 **[擴充事件]** 節點來啟動或停止「擴充事件」工作階段。  
  
 當您停止事件工作階段時，此工作階段不再列為 sys.dm_xe_sessions 動態管理檢視 (DMV) 中的使用中工作階段。 但是，工作階段定義會保持不變，而且您可以重新啟動工作階段。 若要完全移除工作階段定義，您必須刪除工作階段。  
  
 若要啟動或停止「擴充事件」工作階段，您必須擁有 ALTER ANY EVENT SESSION 權限。  
  
 當您停止了使用記憶體中目標 (如信號緩衝區、值區、事件配對或同步事件計數器目標) 的工作階段時，儲存在工作階段緩衝區中的所有資訊 (sys.dm_xe_session_targets DMV 的 target_data 資料行) 都將遺失。 若要在停止工作階段之後存取事件資料，您應該在停止工作階段之前先儲存資料，或是將工作階段設定為使用檔案目標。  
  
### <a name="start-or-stop-an-extended-events-session-using-query-editor"></a>使用查詢編輯器啟動或停止擴充事件工作階段  
 若要啟動工作階段，請發出下列陳述式，使用「擴充事件」工作階段名稱來取代 *session_name* ：  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = START  
```  
  
 若要停止工作階段，請發出下列陳述式，使用「擴充事件」工作階段名稱來取代 *session_name* ：  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = STOP  
```  
  
### <a name="start-or-stop-an-extended-events-session-in-object-explorer"></a>在物件總管中啟動或停止擴充事件工作階段  
 若要在 **[物件總管]** 中啟動或停止「擴充事件」工作階段，請依序展開 **[管理]**、 **[擴充事件]** 和 **[工作階段]** 節點、以滑鼠右鍵按一下工作階段，然後按一下 **[啟動工作階段]** 或 **[停止工作階段]**。  
  
## <a name="export-an-extended-events-session-template"></a>匯出擴充事件工作階段範本  
 您可以使用 **[物件總管]** 來匯出「擴充事件」工作階段，並將它儲存為 .xml 範本檔案。 例如，您可能會想要匯出工作階段，然後使用 **[新增工作階段精靈]** 或 **[新增工作階段]** 精靈，將範本套用到新的事件工作階段。  
  
 當您匯出工作階段時，請務必將範本檔案儲存到使用 NTFS 檔案系統的位置，而且要將存取限制為被授權能夠檢視資訊的使用者。  
  
 若要在 **[物件總管]** 中匯出「擴充事件」工作階段：  
  
1.  依序展開 **[管理]**、 **[擴充事件]** 和 **[工作階段]** 節點。  
  
2.  以滑鼠右鍵按一下您想要匯出的工作階段，然後選取 [匯出工作階段]。  
  
3.  在 **[另存新檔]** 對話方塊中，選取儲存檔案的位置，並在 **[檔案名稱]** 方塊中輸入檔案名稱，然後按一下 **[儲存]**。  
  
     如果您將檔案儲存至預設 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 範本位置，當您使用 **[新增工作階段精靈]** 和 **[新增工作階段]** 對話方塊時，此範本將顯示在預先定義範本的下拉式清單中。  
  
## <a name="import-an-extended-events-session-template"></a>匯入擴充事件工作階段範本  
 您可以使用 **[物件總管]** 來匯入「擴充事件」工作階段的範本。 例如，您可能會想要這樣做，以便根據從另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體匯出的範本建立工作階段。  
  
 若要匯入「擴充事件」工作階段，您必須擁有必要的 **ALTER ANY EVENT SESSION** 權限。  
  
 匯入範本檔案之前，請確定檔案來自信任的來源。 範本檔案應該儲存至使用 NTFS 檔案系統的位置，而且其存取權應該限制為被授權能夠檢視資訊的使用者。  
  
 若要匯入「擴充事件」工作階段：  
  
1.  在 **[物件總管]** 中，依序展開 **[管理]** 和 **[擴充事件]** 節點。  
  
2.  以滑鼠右鍵按一下 [工作階段]，然後選取 [新增工作階段]。  
  
3.  指定工作階段的名稱。  
  
4.  展開 **[範本]** 下拉式方塊。  
  
5.  按一下 [\<檔案來源 …>開啟]，然後巡覽至您想要匯入的工作階段 (XML 檔案)。  
  
 此工作階段會顯示在 **[工作階段]** 節點底下。 根據預設，工作階段不會啟動。  
  
## <a name="edit-an-extended-events-session"></a>編輯擴充事件工作階段  
 您可以在 [物件總管] 中編輯「擴充事件」工作階段。  
  
 若要編輯「擴充事件」工作階段：  
  
1.  在 **[物件總管]** 中，依序展開 **[管理]**、 **[擴充事件]** 和 **[工作階段]** 節點。  
  
2.  以滑鼠右鍵按一下工作階段，然後選取 [屬性]。  
  
3.  在 **[選取頁面]** 區段中，選取要編輯的頁面。  
  
4.  完成事件工作階段的修訂之後，請按一下 **[確定]**。  
  
## <a name="script-an-event-session-definition-using-includetsqlincludestsql-mdmd"></a>使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
 [新增工作階段精靈] 和 [新增工作階段] 對話方塊都具有指令碼選項，可產生定義「擴充事件」工作階段的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 您可以用滑鼠右鍵按一下工作階段名稱、選取 [!INCLUDE[tsql](../../includes/tsql-md.md)] [編寫工作階段的指令碼為] **，然後選取**[CREATE 至] **，藉以存取現有「擴充事件」工作階段的**。  
  
## <a name="delete-an-extended-events-session"></a>刪除擴充事件工作階段  
 您可以刪除「擴充事件」工作階段：  
  
-   在 [查詢編輯器] 中使用 **DROP EVENT SESSION**。  
  
-   在 **[物件總管]** 中。  
  
 當您刪除事件工作階段時，便會移除所有組態資訊，而且工作階段定義不會再出現在 sys.server_event_sessions 目錄檢視中。  
  
> [!NOTE]  
>  system_health 和 Always On_health 都隨附於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請勿刪除它們。 system_health 預設為啟用 (如需詳細資訊，請參閱 [使用 system_health 工作階段](../../relational-databases/extended-events/use-the-system-health-session.md))。 Always On_health 預設為關閉。 這些工作階段會收集可用於診斷效能問題的資料。  
  
 若要刪除「擴充事件」工作階段，您必須擁有 ALTER ANY EVENT SESSION 權限。  
  
 若要在 **[物件總管]** 中刪除「擴充事件」工作階段：  
  
1.  依序展開 **[管理]**、 **[擴充事件]** 和 **[工作階段]** 節點。  
  
2.  以滑鼠右鍵按一下工作階段，然後選取 [刪除]。  
  
3.  在 **[刪除物件]** 對話方塊中，按一下 **[確定]**。  
  
4.  完成事件工作階段的修訂之後，請按一下 **[確定]**。  
  
 若要在 [查詢編輯器] 中刪除「擴充事件」工作階段，請發出下列陳述式，使用您想要刪除的「擴充事件」工作階段名稱來取代 *session_name*：  
  
```  
DROP EVENT SESSION [session_name]  
ON SERVER  
```  
  
  
