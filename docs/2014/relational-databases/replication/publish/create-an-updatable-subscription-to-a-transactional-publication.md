---
title: Create an Updatable Subscription to a Transactional Publication (Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- updateable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f9c04c03c08f118314dc96c8b491e61be317f40c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62691599"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication-management-studio"></a>建立交易式發行集的可更新訂閱 (Management Studio)

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
異動複寫可使用立即或佇列更新訂閱，讓訂閱者上所做的變更傳播回到發行者。 您可以使用複寫預存程序以程式設計的方式建立更新訂閱。

在 [新增訂閱精靈] 的 [可更新訂閱] 頁面上設定可更新訂閱。 此頁面僅在為可更新訂閱啟用了交易式發行集之後才可用。 如需啟用可更新訂閱的詳細資訊，請參閱[啟用交易式發行集的可更新訂閱](enable-updating-subscriptions-for-transactional-publications.md)。   
  
## <a name="configure-an-updatable-subscription-from-the-publisher"></a>從發行者設定可更新訂閱  

1. 連線到 Microsoft SQL Server Management Studio 中的發行者，然後展開伺服器節點。
2. 展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。
3. 以滑鼠右鍵按一下為更新訂閱啟用的交易式發行集，然後按一下 [新增訂閱]。
4. 遵循精靈中的頁面來指定訂閱的選項，例如散發代理程式應在何處執行。
5. 在 [新增訂閱精靈] 的 [可更新的訂閱] 頁面上，確定已選取 [複寫]。
6. 從 [在發行者端認可] 下拉式清單中選取一個選項：

    *  若要使用立即更新訂閱，請選取 [同時認可變更]。 如果您選取這個選項，而且發行集允許佇列更新訂閱 (使用 [新增發行集精靈] 所建立之發行集的預設值)，訂閱屬性 **update_mode** 會設定為 **failover**。 如有必要，這個模式允許您以後可切換至佇列更新。
    *  若要使用佇列更新訂閱，請選取 [佇列變更且盡可能認可]。 如果您選取這個選項，而發行集允許立即更新訂閱 (使用 [新增發行集精靈] 建立之發行集的預設值)，而且訂閱者執行的是 SQL Server 2005 或更新版本，則訂閱屬性 **update_mode** 會設定為 queued failover。 如有必要，這個模式允許您以後可切換至立即更新。

    如需切換更新模式的資訊，請參閱[切換可更新之交易式訂閱的更新模式](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

7. 針對使用立即更新或將 **update_mode** 設定為 **queued failover**，會顯示 [可更新訂閱的登入] 頁面。 在 [可更新訂閱的登入] 頁面上，指定連線到發行者之連結的伺服器，以立即更新訂閱。 在訂閱者端引發的觸發程序，會使用這些連接將變更傳播至發行者。 選取下列其中一個選項：

    * **建立使用 SQL Server 驗證來連線的連結伺服器。** 若您已透過尚未定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。 複寫會為您建立連結伺服器。 您必須指定已存在於發行者的帳戶。
    * **使用您已定義的連結伺服器或遠端伺服器。** 若您已透過 [sp_addserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql)、[sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)、SQL Server Management Studio 或其他方法定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。

    如需連結伺服器帳戶所需權限的資訊，請參閱[在這裡輸入連結描述](../security/secure-the-subscriber.md)的**佇列更新訂閱**。

8. 完成精靈。

## <a name="configure-an-updatable-subscription-from-the-subscriber"></a>從訂閱者設定可更新訂閱


1. 連線到 SQL Server Management Studio 中的訂閱者，然後展開伺服器節點。
2. 展開 **[複寫]** 資料夾。
3. 以滑鼠右鍵按一下 **[區域訂閱]** 資料夾，然後按一下 **[新增訂閱]**。
4. 在 [新增訂閱精靈] 的 [發行集] 頁面上，從 [發行者] 下拉式清單中選取 [<尋找 SQL Server 發行者>]。
5. 連接到 **[連接到伺服器]** 對話方塊中的發行者。
6. 在 [發行集] 頁面上選取為更新訂閱啟用的交易式發行集。
7. 遵循精靈中的頁面來指定訂閱的選項，例如散發代理程式應在何處執行。
8. 在 [新增訂閱精靈] 的 [可更新的訂閱] 頁面上，確定已選取 [複寫]。
9. 從 [在發行者端認可] 下拉式清單中選取一個選項：

    * 若要使用立即更新訂閱，請選取 [同時認可變更]。 如果您選取這個選項，而且發行集允許佇列更新訂閱 (使用 [新增發行集精靈] 所建立之發行集的預設值)，訂閱屬性 **update_mode** 會設定為 **failover**。 如有必要，這個模式允許您以後可切換至佇列更新。
    * 若要使用佇列更新訂閱，請選取 [佇列變更且盡可能認可]。 如果您選取這個選項，而發行集允許立即更新訂閱 (使用 [新增發行集精靈] 建立之發行集的預設值)，而且訂閱者執行的是 SQL Server 2005 或更新版本，則訂閱屬性 **update_mode** 會設定為 **queued failover**。 如有必要，這個模式允許您以後可切換至立即更新。

    如需切換更新模式的資訊，請參閱[切換可更新之交易式訂閱的更新模式](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。

10. 針對使用立即更新或將 **update_mode** 設定為 **queued failover**，會顯示 [可更新訂閱的登入] 頁面。 在 [可更新訂閱的登入] 頁面上，指定連線到發行者之連結的伺服器，以立即更新訂閱。 在訂閱者端引發的觸發程序，會使用這些連接將變更傳播至發行者。 選取下列其中一個選項：

    * **建立使用 SQL Server 驗證來連線的連結伺服器。** 若您已透過尚未定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。 複寫會為您建立連結伺服器。 您必須指定已存在於發行者的帳戶。
    * **使用您已定義的連結伺服器或遠端伺服器。** 若您已透過 [sp_addserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql)、[sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)、SQL Server Management Studio 或其他方法定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。

    如需連結伺服器帳戶所需權限的資訊，請參閱[在這裡輸入連結描述](../security/secure-the-subscriber.md)的**佇列更新訂閱**。

11. 完成精靈。

## <a name="create-an-immediate-updating-pull-subscription"></a>建立立即更新提取訂閱

1. 在發行者上，執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)來確認發行集可支援立即更新訂閱。 

    * 如果結果集中 `allow_sync_tran` 的值為 `1`，則表示發行集可支援立即更新訂閱。
    * 如果結果集中 `allow_sync_tran` 的值為 `0`，則表示必須在啟用立即更新訂閱的情況下重新建立發行集。

2. 在發行者上，執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)來確認發行集可支援提取訂閱。 

    * 如果結果集中 `allow_pull` 的值為 `1`，則表示發行集可支援提取訂閱。
    * 如果 `allow_pull` 的值是 `0`，請執行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，並針對 `allow_pull` 指定 `@property` 、針對 `true` 指定 `@value`。 

3. 在訂閱者上，執行 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)。 指定 `@publisher` 和 `@publication`，並對 `@update_mode`指定下列其中一個值：

    * `sync tran` - 啟用立即更新的訂閱。
    * `failover` - 啟用立即更新的訂閱，且利用佇列更新來做為容錯移轉選項。

    > [!NOTE]  
>  `failover` - 要求也要針對佇列更新訂閱啟用發行集。 
 
4. 在訂閱者上，執行 [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)。 指定下列項目：

    * `@publisher`、 `@publisher_db`和 `@publication` 參數。 
    * Microsoft Windows 認證，「訂閱者」上的「散發代理程式」執行時會針對 `@job_login` 和 `@job_password`使用該認證。 

    > [!NOTE]  
>  使用「Windows 整合式驗證」建立的連接一律使用由 `@job_login` 和 `@job_password`指定的 Windows 認證。 散發代理程式一律使用「Windows 整合式驗證」建立與訂閱者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到散發者。 
 
    * (選擇性) `0` 的 `@distributor_security_mode` 值和 `@distributor_login` 和 `@distributor_password`的 Microsoft SQL Server 登入資訊，如果您需要在連接到散發者時使用 SQL Server 驗證的話。 
    * 此訂閱之散發代理程式作業的排程。 

5. 在訂閱資料庫的訂閱者上，執行 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)。 指定 `@publisher`、 `@publication`、 `@publisher_db`的發行集資料庫名稱，和 `@security_mode`的下列其中一個值： 

    * `0` - 在發行者上進行更新時使用「SQL Server 驗證」。 此選項要求您在發行者上針對 `@login` 和 `@password`指定有效的登入。
    * `1` - 在連接到發行者時，使用在訂閱者上進行變更之使用者的安全性內容。 如需與此安全性模式有關的限制，請參閱 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) 。
    * `2` - 使用透過 [sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)所建立之現有使用者定義的連結伺服器登入。

6. 在發行者上，執行 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) ，並指定 `@publication`、 `@subscriber`、 `@destination_db`、 `@subscription_type`的提取值，以及針對 `@update_mode`指定在步驟 3 中指定的相同值。

這樣會在發行者上註冊提取訂閱。 


## <a name="create-an-immediate-updating-push-subscription"></a>建立立即更新發送訂閱 

1. 在發行者上，執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)來確認發行集可支援立即更新訂閱。 

    * 如果結果集中 `allow_sync_tran` 的值為 `1`，則表示發行集可支援立即更新訂閱。
    * 如果結果集中 `allow_sync_tran` 的值為 `0`，則表示必須在啟用立即更新訂閱的情況下重新建立發行集。

2. 在發行者上，執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)來確認發行集可支援發送訂閱。 

    * 如果結果集中 `allow_push` 的值為 `1`，則表示發行集可支援發送訂閱。
    * 如果 `allow_push` 的值是 `0`，請執行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，並針對 `allow_push` 指定 `@property` 、針對 `true` 指定 `@value`。 

3. 在發行者上，執行 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)。 指定 `@publication`、 `@subscriber`、 `@destination_db`，並對 `@update_mode`指定下列其中一個值：

    * `sync tran` - 啟用立即更新的支援。
    * `failover` - 啟用立即更新的支援，並將佇列更新當做容錯移轉選項。

    > [!NOTE]  
>  `failover` - 要求也要針對佇列更新訂閱啟用發行集。 
 
4. 在發行者上，執行 [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)。 指定下列參數：

    * `@subscriber``@subscriber_db`和 `@publication`。 
    * 散發代理程式在散發者上執行時，針對 `@job_login` 和 `@job_password`所使用的 Windows 認證。 

    > [!NOTE]  
>  使用「Windows 整合式驗證」建立的連接一律使用由 `@job_login` 和 `@job_password`指定的 Windows 認證。 散發代理程式一律使用「Windows 整合式驗證」建立與散發者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到訂閱者。 

    * (選擇性) `0` 的 `@subscriber_security_mode` 值和 `@subscriber_login` 和 `@subscriber_password`的 SQL Server 登入資訊，如果您需要在連接到訂閱者時使用 SQL Server 驗證的話。 
    * 此訂閱之散發代理程式作業的排程。

5. 在訂閱資料庫的訂閱者上，執行 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)。 指定 `@publisher`、 `@publication`、 `@publisher_db`的發行集資料庫名稱，和 `@security_mode`的下列其中一個值： 

     * `0` - 在發行者上進行更新時使用「SQL Server 驗證」。 此選項要求您在發行者上針對 `@login` 和 `@password`指定有效的登入。
     * `1` - 在連接到發行者時，使用在訂閱者上進行變更之使用者的安全性內容。 如需與此安全性模式有關的限制，請參閱 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) 。
     * `2` - 使用透過 [sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)所建立之現有使用者定義的連結伺服器登入。


## <a name="create-a-queued-updating-pull-subscription"></a>建立佇列更新提取訂閱 ##

1. 在發行者上，執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)來確認發行集可支援佇列更新訂閱。 

    * 如果結果集中 `allow_queued_tran` 的值為 `1`，則表示發行集可支援立即更新訂閱。
    * 如果結果集中 `allow_queued_tran` 的值為 `0`，則表示必須在啟用佇列更新訂閱的情況下重新建立發行集。

2. 在發行者上，執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)來確認發行集可支援提取訂閱。 

    * 如果結果集中 `allow_pull` 的值為 `1`，則表示發行集可支援提取訂閱。
    * 如果 `allow_pull` 的值是 `0`，請執行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，並針對 `allow_pull` 指定 `@property` 、針對 `true` 指定 `@value`。 

3. 在訂閱者上，執行 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)。 指定 `@publisher` 和 `@publication`，並對 `@update_mode`指定下列其中一個值：

    * `queued tran` - 啟用佇列更新的訂閱。
    * `queued failover` - 啟用佇列更新的支援，並將立即更新當作容錯移轉選項。

    > [!NOTE]  
>  `queued failover` - 要求也要針對立即更新訂閱啟用發行集。 若要容錯移轉到立即更新，您必須使用 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) ，以定義訂閱者上的變更複寫到發行者時所用的認證。
 
4. 在訂閱者上，執行 [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)。 指定下列參數：

    * @publisher`@publisher_db`和 `@publication`。 
    * Windows 認證，「訂閱者」上的「散發代理程式」執行時會針對 `@job_login` 和 `@job_password`使用該認證。 

    > [!NOTE]  
>  使用「Windows 整合式驗證」建立的連接一律使用由 `@job_login` 和 `@job_password`指定的 Windows 認證。 散發代理程式一律使用「Windows 整合式驗證」建立與訂閱者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到散發者。 
 
    * (選擇性) `0` 的 `@distributor_security_mode` 值和 `@distributor_login` 和 `@distributor_password`的 SQL Server 登入資訊，如果您需要在連接到散發者時使用 SQL Server 驗證的話。 
    * 此訂閱之散發代理程式作業的排程。

5. 在發行者上，執行 [sp_addsubscriber](/sql/relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql) ，在發行者註冊訂閱者，並指定 `@publication`、 `@subscriber`、 `@destination_db`、 `@subscription_type`的提取值，以及針對 `@update_mode`指定在步驟 3 中指定的相同值。

這樣會在發行者上註冊提取訂閱。 


## <a name="to-create-a-queued-updating-push-subscription"></a>建立佇列更新發送訂閱 ##

1. 在發行者上，執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)來確認發行集可支援佇列更新訂閱。 

    * 如果結果集中 allow_queued_tran 的值為 1，則表示發行集可支援立即更新訂閱。
    * 如果結果集中 allow_queued_tran 的值為 0，則表示必須在啟用佇列更新訂閱的情況下重新建立發行集。 如需詳細資訊，請參閱＜如何：啟用交易式發行集的可更新訂閱 (複寫 Transact-SQL 程式設計)＞。

2. 在發行者上，執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)來確認發行集可支援發送訂閱。 

    * 如果結果集中 `allow_push` 的值為 `1`，則表示發行集可支援發送訂閱。
    * 如果 `allow_push` 的值是 `0`，請執行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，並針對 `@property` 指定 allow_push、針對 `true` 指定 `@value`。 

3. 在發行者上，執行 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)。 指定 `@publication`、 `@subscriber`、 `@destination_db`，並對 `@update_mode`指定下列其中一個值：

    * `queued tran` - 啟用佇列更新的訂閱。
    * `queued failover` - 啟用佇列更新的支援，並將立即更新當作容錯移轉選項。

    > [!NOTE]  
>  queued failover 選項要求也要針對立即更新訂閱啟用發行集。 若要容錯移轉到立即更新，您必須使用 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) ，以定義訂閱者上的變更複寫到發行者時所用的認證。

4. 在發行者上，執行 [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)。 指定下列參數：

    * `@subscriber``@subscriber_db`和 `@publication`。 
    * 散發代理程式在散發者上執行時，針對 `@job_login` 和 `@job_password`所使用的 Windows 認證。 

    > [!NOTE]  
>  使用「Windows 整合式驗證」建立的連接一律使用由 `@job_login` 和 `@job_password`指定的 Windows 認證。 散發代理程式一律使用「Windows 整合式驗證」建立與散發者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到訂閱者。 
 
    * (選擇性) `0` 的 `@subscriber_security_mode` 值和 `@subscriber_login` 和 `@subscriber_password`的 SQL Server 登入資訊，如果您需要在連接到訂閱者時使用 SQL Server 驗證的話。 
    * 此訂閱之散發代理程式作業的排程。


## <a name="example"></a>範例 ##

此範例會建立發行集的立即更新提取訂閱，此發行集可支援立即更新訂閱。 登入和密碼值是在執行階段使用 sqlcmd 指令碼變數提供的。

> [!NOTE]  
>  此指令碼使用 sqlcmd 指令碼變數。 它們的格式為 `$(MyVariable)`。 如需如何在命令列和 SQL Server Management Studio 中，使用指令碼變數的詳細資訊，請參閱[複寫系統預存程序概念](../concepts/replication-system-stored-procedures-concepts.md)主題中的＜執行複寫指令碼＞一節。

```sql
-- Execute this batch at the Subscriber.
DECLARE @publication AS sysname;
DECLARE @publicationDB AS sysname;
DECLARE @publisher AS sysname;
DECLARE @login AS sysname;
DECLARE @password AS nvarchar(512);
SET @publication = N'AdvWorksProductTran';
SET @publicationDB = N'AdventureWorks2008R2';
SET @publisher = $(PubServer);
SET @login = $(Login);
SET @password = $(Password);

-- At the subscription database, create a pull subscription to a transactional 
-- publication using immediate updating with queued updating as a failover.
EXEC sp_addpullsubscription 
    @publisher = @publisher, 
    @publication = @publication, 
    @publisher_db = @publicationDB, 
    @update_mode = N'failover', 
    @subscription_type = N'pull';

-- Add an agent job to synchronize the pull subscription, 
-- which uses Windows Authentication when connecting to the Distributor.
EXEC sp_addpullsubscription_agent 
    @publisher = @publisher, 
    @publisher_db = @publicationDB, 
    @publication = @publication,
    @job_login = @login,
    @job_password = @password; 

-- Add a Windows Authentication-based linked server that enables the 
-- Subscriber-side triggers to make updates at the Publisher. 
EXEC sp_link_publication 
    @publisher = @publisher, 
    @publication = @publication,
    @publisher_db = @publicationDB, 
    @security_mode = 0,
    @login = @login,
    @password = @password;
GO

USE AdventureWorks2008R2;
GO

-- Execute this batch at the Publisher.
DECLARE @publication AS sysname;
DECLARE @subscriptionDB AS sysname;
DECLARE @subscriber AS sysname;
SET @publication = N'AdvWorksProductTran'; 
SET @subscriptionDB = N'AdventureWorks2008R2Replica'; 
SET @subscriber = $(SubServer);

-- At the Publisher, register the subscription, using the defaults.
USE [AdventureWorks2008R2]
EXEC sp_addsubscription 
    @publication = @publication, 
    @subscriber = @subscriber, 
    @destination_db = @subscriptionDB, 
    @subscription_type = N'pull', 
    @update_mode = N'failover';
GO
```

## <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>設定佇列更新衝突解決選項 (SQL Server Management Studio)
  在 [發行集屬性 - \<發行集>] 對話方塊的 [訂閱選項] 頁面中，為支援佇列更新訂閱的發行集設定衝突解決選項。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](view-and-modify-publication-properties.md)＞。  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>若要設定佇列更新衝突解決選項  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [訂閱選項] 頁面中，選取下列 [衝突解決原則] 選項的其中一個值︰    
    -   **[保留發行者變更]**    
    -   **[保留訂閱者變更]**    
    -   **[重新初始化訂閱]**    
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="see-also"></a>另請參閱 ##
 [Create a Publication](create-a-publication.md)   
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)   
 [以指令碼變數使用 sqlcmd](../../scripting/sqlcmd-use-with-scripting-variables.md)   

  
