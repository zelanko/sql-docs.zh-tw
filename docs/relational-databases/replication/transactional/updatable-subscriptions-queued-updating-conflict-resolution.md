---
title: 佇列更新衝突偵測和解決 | Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- viewing queued updating conflicts
- conflict resolution [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
- articles [SQL Server replication], conflict resolution
ms.assetid: 084ac587-25e7-4bd0-a385-556bbe07d02f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b2bc4cf6348180e52dea28698e90cafda4f32f79
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67895485"
---
# <a name="updatable-subscriptions---queued-updating-conflict-resolution"></a>可更新訂閱 - 佇列更新衝突解決方法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  因為佇列更新訂閱允許在多個位置對相同資料做修改，則在發行者同步資料時，有可能發生衝突。 複寫會在變更與發行者同步處理時偵測是否有任何衝突，並使用您在建立發行集時選取的解決原則解決衝突。 會發生下列衝突：  
  
-   更新與插入衝突。 當相同的資料在兩個位置同時變更時，就會發生此衝突。 一個變更成功，而另一個變更失敗。  
  
-   刪除衝突。 當資料列在一處已遭刪除，而在另一處已被更新，就會發生此衝突。  
  
 衝突偵測和解決可能是相當耗時間且需使用相當多資源的程序；因此，最好在應用程式中藉由建立資料分割的方式將衝突減至最少，這種方式可讓不同的訂閱者修改不同的資料子集。  
  
## <a name="detecting-conflicts"></a>偵測衝突  
 建立發行集和啟用佇列更新時，複寫會將預設值是 **newid()** 的**uniqueidentifier**資料行 ( **msrepl_tran_version** ) 加入基礎資料表中。 當發行的資料是在發行者或訂閱者變更，資料列會接收全域唯一識別碼 (GUID) 來指示新的資料列版本存在。 「佇列讀取器代理程式」會在同步時使用此資料行，判斷衝突是否存在。  
  
 佇列中的交易會維護新舊的值。 在發行者套用交易時，交易的 GUID 以及發行集內的 GUID 會相互比較。 若儲存在交易中的 GUID 符合發行集內的 GUID，就會更新發行集而且會指派由訂閱者產生的資料列。 將發行集更新成交易中的 GUID 後，您在發行集和交易中有相符的資料列。  
  
 若儲存在交易中的舊 GUID 不符合發行集內的 GUID，就會偵測到衝突。 發行集內的新 GUID 指示有兩種不同的資料列版本存在：訂閱者傳送之交易中的 GUID，另一個是存在於發行者較新的 GUID。 在此狀況下，會在此訂閱者交易同步之前，另一個訂閱者或發行者會先更新發行集內同一個資料列。  
  
 與合併式複寫不同的是，使用 GUID 資料行並不是用來識別資料列本身，而是用來檢查資料列是否變更。  
  
## <a name="resolving-conflicts"></a>解決衝突  
 當您使用佇列更新建立發行集時，會選取要在偵測到任何衝突時使用的衝突解決器。 衝突解決器會管理「佇列讀取器代理程式」進行同步處理過程中所遭遇不同版本之同一資料列的方式。 只要沒有訂閱發行集時，就可以在建立發行集後變更衝突解決原則。 衝突解決器選擇如下：  
  
-   發行者優先 (預設值)  
  
-   發行者優先且重新初始化訂閱  
  
-   訂閱者優先  
  
 衝突可以使用「衝突檢視器」來記錄和檢視。  
  
 **若要設定佇列更新衝突解決原則**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：[ &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
-   複寫 Transact-SQL 程式設計： [啟用交易式發行集的更新訂閱](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
 **若要檢視資料衝突**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：[View Data Conflicts for Transactional Publications &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md) (檢視交易式發行集的資料衝突 &#40;SQL Server Management Studio&#41;)  
  
### <a name="publisher-wins"></a>發行者優先  
 當衝突解決設定成「發行者優先」時，會以發行者的資料為基礎來維護交易一致性。 衝突中的交易會在初始它的訂閱者復原。  
  
 「佇列讀取器代理程式」會偵測衝突，且會產生補償的命令，並張貼於散發資料庫中藉此將其傳播至訂閱者。 之後，「散發代理程式」會將補償命令套用至產生衝突交易的訂閱者。 補償動作會更新訂閱者上的資料列，使其符合發行者上的資料列。  
  
 直到套用補償命令之前，您都可以讀取最終會於訂閱者回復的交易結果。 這相當於中途讀取 (讀取未認可隔離等級)。 針對可能發生的後續相關交易則無任何補償。 不過，交易界限將被接受，而交易中的所有動作都會經過認可，或於發生衝突時回復。  
  
### <a name="publisher-wins-and-the-subscription-is-reinitialized"></a>發行者優先且重新初始化訂閱  
 重新初始化訂閱者來解決衝突，可以維護訂閱者的交易一致性，不過若發行集包含大量的資料，就會耗費大量時間。  
  
 當「佇列讀取器代理程式」偵測到衝突，佇列中所有剩餘交易 (包括衝突中的交易) 會遭到拒絕，而且訂閱者會標示著重新初始化。 為發行集產生的下一個快照集是由「散發代理程式」套用到訂閱者。  
  
### <a name="subscriber-wins"></a>訂閱者優先  
 訂閱者優先原則下的衝突偵測意謂最後要更新訂閱者優先的訂閱者交易。 在此狀況下，當偵測到衝突的時候，仍然會使用訂閱者傳送的交易並且會更新發行者。 此原則適用於類似變更無法符合資料完整性的應用程式。  
  
## <a name="see-also"></a>另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
