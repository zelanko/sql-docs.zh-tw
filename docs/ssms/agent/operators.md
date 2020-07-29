---
title: 操作員
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- operators (users) [Database Engine]
- fail-safe operator [SQL Server]
- aliases [SQL Server], operators
- SQL Server Agent alerts, operators
- contact information [SQL Server Agent]
- net send [SQL Server]
- e-mail [SQL Server], SQL Server Agent operators
- pager notifications [SQL Server Agent]
- mail [SQL Server], SQL Server Agent operators
- operators (users) [Database Engine], defining
- jobs [SQL Server Agent], operators
- alerts [SQL Server], operators
ms.assetid: 38e8488f-2669-4cea-b9c3-5f394a663678
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a500a4c03562d024bb64a65053fe1afc374844c8
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246437"
---
# <a name="operators"></a>運算子
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

操作員是人員或群組的別名，當作業完成或產生警示時，可收到電子通知。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務可支援透過操作員，發送通知給系統管理員。 操作員會啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的通知和監視功能。  
  
## <a name="operator-attributes-and-concepts"></a>操作員屬性和概念  
操作員的主要屬性如下：  
  
-   操作員名稱  
  
-   連絡人資訊  
  
### <a name="naming-an-operator"></a>為操作員命名  
每個操作員都必須要有一個名稱。 操作員名稱必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中唯一的名稱，而且不可長於 **128** 個字元。  
  
### <a name="contact-information"></a>連絡資訊  
操作員的連絡資訊會定義如何通知操作員。 您可以透過電子郵件、呼叫器或 **net send** 命令來通知操作員：  
  
> [!IMPORTANT]
> 呼叫器和 **net send** 選項會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未來版本的 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。  
  
-   **電子郵件通知**  
  
    電子郵件通知會傳送電子郵件訊息給操作員。 若是使用電子郵件通知，您需提供操作員的電子郵件地址。  
  
-   **呼叫器通知**  
  
    呼叫是透過電子郵件來實作的。 若是使用呼叫器通知，您需提供操作員用來接收呼叫器訊息的電子郵件地址。 若要設定呼叫器通知，您必須將軟體安裝在郵件伺服器上，以便處理傳入郵件，並將其轉換為呼叫器訊息。 該軟體可以採取幾種方法之一，包括：  
  
    -   將郵件轉寄到位於呼叫器供應商站台的遠端郵件伺服器。  
  
        雖然所需的軟體一般都存在於本機郵件系統而可以使用，但是呼叫器供應商必須提供這項服務。 如需詳細資訊，請參閱您的呼叫器文件集。  
  
    -   透過 Internet，將電子郵件路由傳送到位於呼叫器供應商站台的電子郵件伺服器。  
  
        這是第一個方法的另一種做法。  
  
    -   處理傳入電子郵件，並使用連接的數據機來撥接呼叫器。  
  
        這個軟體是呼叫器服務供應商的專利。 這個軟體的作用像是電子郵件用戶端，可將所有或部分電子郵件地址資訊解譯成呼叫器號碼，或是將電子郵件名稱對應到轉換表中的呼叫器號碼，以定期處理其收件匣。  
  
        如果所有的操作員共用同一個呼叫器供應商，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來指定呼叫器轉電子郵件系統所需的任何特殊電子郵件格式。 此特殊格式可以是前置詞或後置詞，並可包含在下列的電子郵件字行中：  
  
        **主體：**  
  
        副本：  
  
        **收件者**：  
  
    > [!NOTE]  
    > 如果使用低容量的英數字元呼叫系統，您可以將呼叫器通知中的錯誤文字排除，以縮短所傳送的文字。 例如，有一種低容量英數字元呼叫系統，每頁限制為 64 個字元。  
  
-   **net sendnotification**  
  
    這是利用 **net send** 命令來將訊息傳送給操作員。 若是使用 **net send**，請指定網路訊息的收件者 (電腦或使用者)。  
  
    > [!NOTE]  
    > **Net send** 命令會使用 Microsoft Windows Messenger。 為了順利傳送警示，執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦和操作員所使用的電腦上，都必須執行此服務。  
  
## <a name="alerting-and-fail-safe-operators"></a>警示及保全操作員  
您可以選擇要告知的操作員來回應警示。 例如，您可以排定警示，來指派操作員通知的輪替責任區分。 例如，發生於星期一、星期三或星期五的警示會告知「人員 A」，而發生於星期二、星期四或星期六的警示則會告知「人員 B」。  
  
如果所有要傳送給指定操作員的呼叫器通知都失敗，保全操作員就會收到警示通知。 例如，如果您已經定義三個呼叫器告知的操作員，但是沒有一個指定的操作員可以呼叫成功，那麼將會告知保全操作員。  
  
發生下列狀況時，會通知保全操作員：  
  
-   無法呼叫到負責警示的操作員。  
  
    連絡主要操作員會失敗的原因，包括：呼叫器號碼錯誤，以及操作員已下班。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 無法存取 **msdb** 資料庫中的系統資料表。  
  
    **sysnotifications** 系統資料表指定負責警示的操作員。  
  
保全操作員是一種安全功能。 若您要刪除負有保全任務的操作員，您必須先將保全任務重新指派給另一個操作員，或是刪除整個保全指派任務。  
  
## <a name="notifying-an-operator"></a>通知操作員  
您必須設定下列一項或多項，才能通知操作員：  
  
-   若要使用 Database Mail 功能來傳送電子郵件，您必須能夠存取支援 SMTP 的電子郵件伺服器。  
  
-   若是使用呼叫器，您必須要有協力廠商呼叫器轉電子郵件的軟體及/或硬體。  
  
-   若要使用 **net send**，操作員必須登入指定的電腦，而指定的電腦必須能夠接受來自 Windows Messenger 的訊息。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作|主題|  
|-|-|  
|與建立操作員相關的工作|[建立操作員](../../ssms/agent/create-an-operator.md)<br /><br />[Designate a Fail-Safe Operator](../../ssms/agent/designate-a-fail-safe-operator.md)|  
|與指派警示相關的工作|[指派警示給操作員](../../ssms/agent/assign-alerts-to-an-operator.md)<br /><br />[定義對警示的回應 &#40;SQL Server Management Studio&#41;](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)<br /><br />[sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)<br /><br />[指派警示給操作員](../../ssms/agent/assign-alerts-to-an-operator.md)|  
  
## <a name="see-also"></a>另請參閱  
[Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
