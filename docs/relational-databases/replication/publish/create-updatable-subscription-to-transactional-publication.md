---
title: "建立交易式發行集的可更新訂閱 | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updateable transactional subscriptions, T-SQL
ms.assetid: a6e80857-0a69-4867-b6b7-f3629d00c312
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7e21ddca2057879f3f9cde2bf5decf3c97944269
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="create-updatable-subscription-to-transactional-publication"></a>建立交易式發行集的可更新訂閱

> [!NOTE]  
>  這項功能在 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 2012 到 2016 的版本中仍然受到支援。  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
異動複寫可使用立即或佇列更新訂閱，讓訂閱者上所做的變更傳播回到發行者。 您可以使用複寫預存程序以程式設計的方式建立更新訂閱。 (此外，請參閱 [建立交易式發行集的可更新訂閱 (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)。) 

## <a name="to-create-an-immediate-updating-pull-subscription"></a>建立立即更新提取訂閱 ##

1. 在發行者上，執行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)來確認發行集可支援立即更新訂閱。 

    * 如果結果集中 `allow_sync_tran` 的值為 `1`，則表示發行集可支援立即更新訂閱。

    * 如果結果集中 `allow_sync_tran` 的值為 `0`，則表示必須在啟用立即更新訂閱的情況下重新建立發行集。

2. 在發行者上，執行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)來確認發行集可支援提取訂閱。 

    * 如果結果集中 `allow_pull` 的值為 `1`，則表示發行集可支援提取訂閱。

    * 如果 `allow_pull` 的值是 `0`，請執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)，並針對 `allow_pull` 指定 `@property` 、針對 `true` 指定 `@value`。 

3. 在訂閱者上，執行 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)。 指定 `@publisher` 和 `@publication`，並對 `@update_mode`指定下列其中一個值：

    * `sync tran` - 啟用立即更新的訂閱。

    * `failover` - 啟用立即更新的訂閱，且利用佇列更新來做為容錯移轉選項。

    > [!NOTE]  
>  `failover` - 要求也要針對佇列更新訂閱啟用發行集。 
 
4. 在訂閱者上，執行 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定下列項目：

    * `@publisher`、 `@publisher_db`和 `@publication` 參數。 

    * Microsoft Windows 認證，「訂閱者」上的「散發代理程式」執行時會針對 `@job_login` 和 `@job_password`使用該認證。 

    > [!NOTE]  
>  使用「Windows 整合式驗證」建立的連接一律使用由 `@job_login` 和 `@job_password`指定的 Windows 認證。 散發代理程式一律使用「Windows 整合式驗證」建立與訂閱者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到散發者。 
 
    * (選擇性) `0` 的 `@distributor_security_mode` 值和 `@distributor_login` 和 `@distributor_password`的 Microsoft SQL Server 登入資訊，如果您需要在連接到散發者時使用 SQL Server 驗證的話。 

    * 此訂閱之散發代理程式作業的排程。 

5. 在訂閱資料庫的訂閱者上，執行 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)。 指定 `@publisher`、 `@publication`、 `@publisher_db`的發行集資料庫名稱，和 `@security_mode`的下列其中一個值： 

    * `0` - 在發行者上進行更新時使用「SQL Server 驗證」。 此選項要求您在發行者上針對 `@login` 和 `@password`指定有效的登入。

    * `1` - 在連接到發行者時，使用在訂閱者上進行變更之使用者的安全性內容。 如需與此安全性模式有關的限制，請參閱 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 。

    * `2` - 使用透過 [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)所建立之現有使用者定義的連結伺服器登入。

6. 在發行者上，執行 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) ，並指定 `@publication`、 `@subscriber`、 `@destination_db`、 `@subscription_type`的提取值，以及針對 `@update_mode`指定在步驟 3 中指定的相同值。

這樣會在發行者上註冊提取訂閱。 


## <a name="to-create-an-immediate-updating-push-subscription"></a>建立立即更新發送訂閱 ##

1. 在發行者上，執行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)來確認發行集可支援立即更新訂閱。 

    * 如果結果集中 `allow_sync_tran` 的值為 `1`，則表示發行集可支援立即更新訂閱。

    * 如果結果集中 `allow_sync_tran` 的值為 `0`，則表示必須在啟用立即更新訂閱的情況下重新建立發行集。

2. 在發行者上，執行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)來確認發行集可支援發送訂閱。 

    * 如果結果集中 `allow_push` 的值為 `1`，則表示發行集可支援發送訂閱。

    * 如果 `allow_push` 的值是 `0`，請執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)，並針對 `allow_push` 指定 `@property` 、針對 `true` 指定 `@value`。 

3. 在發行者上，執行 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定 `@publication`、 `@subscriber`、 `@destination_db`，並對 `@update_mode`指定下列其中一個值：

    * `sync tran` - 啟用立即更新的支援。

    * `failover` - 啟用立即更新的支援，並將佇列更新當做容錯移轉選項。

    > [!NOTE]  
>  `failover` - 要求也要針對佇列更新訂閱啟用發行集。 
 
4. 在發行者上，執行 [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)。 指定下列參數：

    * `@subscriber``@subscriber_db`和 `@publication`。 

    * 散發代理程式在散發者上執行時，針對 `@job_login` 和 `@job_password`所使用的 Windows 認證。 

    > [!NOTE]  
>  使用「Windows 整合式驗證」建立的連接一律使用由 `@job_login` 和 `@job_password`指定的 Windows 認證。 散發代理程式一律使用「Windows 整合式驗證」建立與散發者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到訂閱者。 

    * (選擇性) `0` 的 `@subscriber_security_mode` 值和 `@subscriber_login` 和 `@subscriber_password`的 SQL Server 登入資訊，如果您需要在連接到訂閱者時使用 SQL Server 驗證的話。 

    * 此訂閱之散發代理程式作業的排程。

5. 在訂閱資料庫的訂閱者上，執行 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)。 指定 `@publisher`、 `@publication`、 `@publisher_db`的發行集資料庫名稱，和 `@security_mode`的下列其中一個值： 

     * `0` - 在發行者上進行更新時使用「SQL Server 驗證」。 此選項要求您在發行者上針對 `@login` 和 `@password`指定有效的登入。

     * `1` - 在連接到發行者時，使用在訂閱者上進行變更之使用者的安全性內容。 如需與此安全性模式有關的限制，請參閱 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 。

     * `2` - 使用透過 [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)所建立之現有使用者定義的連結伺服器登入。


## <a name="to-create-a-queued-updating-pull-subscription"></a>建立佇列更新提取訂閱 ##

1. 在發行者上，執行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)來確認發行集可支援佇列更新訂閱。 

    * 如果結果集中 `allow_queued_tran` 的值為 `1`，則表示發行集可支援立即更新訂閱。

    * 如果結果集中 `allow_queued_tran` 的值為 `0`，則表示必須在啟用佇列更新訂閱的情況下重新建立發行集。

2. 在發行者上，執行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)來確認發行集可支援提取訂閱。 

    * 如果結果集中 `allow_pull` 的值為 `1`，則表示發行集可支援提取訂閱。

    * 如果 `allow_pull` 的值是 `0`，請執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)，並針對 `allow_pull` 指定 `@property` 、針對 `true` 指定 `@value`。 

3. 在訂閱者上，執行 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)。 指定 `@publisher` 和 `@publication`，並對 `@update_mode`指定下列其中一個值：

    * `queued tran` - 啟用佇列更新的訂閱。

    * `queued failover` - 啟用佇列更新的支援，並將立即更新當作容錯移轉選項。

    > [!NOTE]  
>  `queued failover` - 要求也要針對立即更新訂閱啟用發行集。 若要容錯移轉到立即更新，您必須使用 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) ，以定義訂閱者上的變更複寫到發行者時所用的認證。
 
4. 在訂閱者上，執行 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定下列參數：

    * @publisher`@publisher_db`和 `@publication`。 

    * Windows 認證，「訂閱者」上的「散發代理程式」執行時會針對 `@job_login` 和 `@job_password`使用該認證。 

    > [!NOTE]  
>  使用「Windows 整合式驗證」建立的連接一律使用由 `@job_login` 和 `@job_password`指定的 Windows 認證。 散發代理程式一律使用「Windows 整合式驗證」建立與訂閱者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到散發者。 
 
    * (選擇性) `0` 的 `@distributor_security_mode` 值和 `@distributor_login` 和 `@distributor_password`的 SQL Server 登入資訊，如果您需要在連接到散發者時使用 SQL Server 驗證的話。 

    * 此訂閱之散發代理程式作業的排程。

5. 在發行者上，執行 [sp_addsubscriber](../../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md) ，在發行者註冊訂閱者，並指定 `@publication`、 `@subscriber`、 `@destination_db`、 `@subscription_type`的提取值，以及針對 `@update_mode`指定在步驟 3 中指定的相同值。

這樣會在發行者上註冊提取訂閱。 


## <a name="to-create-a-queued-updating-push-subscription"></a>建立佇列更新發送訂閱 ##

1. 在發行者上，執行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)來確認發行集可支援佇列更新訂閱。 

    * 如果結果集中 allow_queued_tran 的值為 1，則表示發行集可支援立即更新訂閱。

    * 如果結果集中 allow_queued_tran 的值為 0，則表示必須在啟用佇列更新訂閱的情況下重新建立發行集。 如需詳細資訊，請參閱＜如何：啟用交易式發行集的可更新訂閱 (複寫 Transact-SQL 程式設計)＞。

2. 在發行者上，執行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)來確認發行集可支援發送訂閱。 

    * 如果結果集中 `allow_push` 的值為 `1`，則表示發行集可支援發送訂閱。

    * 如果 `allow_push` 的值是 `0`，請執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)，並針對 `@property` 指定 allow_push、針對 `true` 指定 `@value`。 

3. 在發行者上，執行 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定 `@publication`、 `@subscriber`、 `@destination_db`，並對 `@update_mode`指定下列其中一個值：

    * `queued tran` - 啟用佇列更新的訂閱。

    * `queued failover` - 啟用佇列更新的支援，並將立即更新當作容錯移轉選項。

    > [!NOTE]  
>  queued failover 選項要求也要針對立即更新訂閱啟用發行集。 若要容錯移轉到立即更新，您必須使用 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) ，以定義訂閱者上的變更複寫到發行者時所用的認證。

4. 在發行者上，執行 [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)。 指定下列參數：

    * `@subscriber``@subscriber_db`和 `@publication`。 

    * 散發代理程式在散發者上執行時，針對 `@job_login` 和 `@job_password`所使用的 Windows 認證。 

    > [!NOTE]  
>  使用「Windows 整合式驗證」建立的連接一律使用由 `@job_login` 和 `@job_password`指定的 Windows 認證。 散發代理程式一律使用「Windows 整合式驗證」建立與散發者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到訂閱者。 
 
    * (選擇性) `0` 的 `@subscriber_security_mode` 值和 `@subscriber_login` 和 `@subscriber_password`的 SQL Server 登入資訊，如果您需要在連接到訂閱者時使用 SQL Server 驗證的話。 

    * 此訂閱之散發代理程式作業的排程。


## <a name="example"></a>範例 ##

此範例會建立發行集的立即更新提取訂閱，此發行集可支援立即更新訂閱。 登入和密碼值是在執行階段使用 sqlcmd 指令碼變數提供的。

> [!NOTE]  
>  此指令碼使用 sqlcmd 指令碼變數。 它們的格式為 `$(MyVariable)`。 如需如何在命令列和 SQL Server Management Studio 中，使用指令碼變數的詳細資訊，請參閱[複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)主題中的＜執行複寫指令碼＞一節。

```
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

## <a name="see-also"></a>另請參閱 ##

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[以指令碼變數使用 sqlcmd](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)

[建立交易式發行集的可更新訂閱 (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)


