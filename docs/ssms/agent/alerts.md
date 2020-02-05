---
title: 警示
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, event types
- SQL Server Agent alerts, names
- alerts [SQL Server], performance conditions
- alerts [SQL Server], about alerts
- WMI event responses [SQL Server Agent alerts]
- events [WMI]
- performance condition alerts [SQL Server Agent]
- alerts [SQL Server], event types
- SQL Server Agent alerts, performance conditions
- SQL Server Agent alerts, about alerts
- alerts [SQL Server], names
ms.assetid: 3f57d0f0-4781-46ec-82cd-b751dc5affef
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b88680cb965ff44384d54b09e0c7244a074bd0db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75252690"
---
# <a name="alerts"></a>警示

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

事件會由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生，並輸入 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 應用程式記錄檔中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會讀取應用程式記錄檔，然後比較寫入其中的事件與您所定義的警示。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 找到相符項目時，即會發出警示，這是對事件的自動回應。 除了監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件以外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 還可以監視效能條件與 Windows Management Instrumentation (WMI) 事件。  
  
若要定義警示，您必須指定：  
  
-   警示的名稱。  
  
-   觸發警示的事件或效能條件。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 為回應事件或效能條件所採取的動作。  
  
## <a name="naming-an-alert"></a>為警示命名  
每個警示必須有一個名稱。 警示名稱在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體中必須是唯一的，而且不可超過 **128** 個字元。  
  
## <a name="selecting-an-event-type"></a>選取事件類型  
警示會回應特定的事件類型。 警示會回應下列事件類型：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 效能條件  
  
-   WMI 事件  
  
事件類型將決定您用來指定精確事件的參數。  
  
## <a name="specifying-a-sql-server-event"></a>指定 SQL Server 事件  
您可以指定要發生的警示，以回應一或多個事件。 請使用下列參數來指定可觸發警示的事件：  
  
-   **錯誤號碼**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會在特定錯誤發生時發出警示。 例如，您可以指定錯誤號碼 2571 來回應對「資料庫主控命令 (DBCC)」的未經授權叫用嘗試。  
  
-   **嚴重性層級**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會在特定嚴重性的任何錯誤發生時發出警示。 例如，您可以指定嚴重性層級 15 來回應 Transact-SQL 陳述式中的語法錯誤。  
  
-   **Database**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 只有在特定資料庫中發生事件時，才會發出警示。 您可以在錯誤號碼或嚴重性層級以外搭配套用此選項。 例如，若某個執行個體中含有一個實際執行用的資料庫和一個報告用的資料庫，您就可以定義一個只會針對實際資料庫回應語法錯誤的警示。  
  
-   **事件文字**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會在指定事件的事件訊息中含有特定的文字字串時發出警示。 例如，您可以定義警示來回應含有特定資料表名稱或特定條件約束名稱的訊息。  
  
## <a name="selecting-a-performance-condition"></a>選取效能條件  
您可以指定一個為回應特定效能條件而產生的警示。 此時您必須指定所要監視的效能計數器、警示的臨界值以及計數器在警示產生時必須顯示的行為。 若要設定效能條件，您必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 [一般]  頁面上定義 [新增警示]  或 [警示屬性]  對話方塊中的下列項目：  
  
-   **Object**  
  
    此物件為要監視的效能區域。  
  
-   **計數器**  
  
    計數器是要監視之區域的屬性。  
  
-   **執行個體**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可為要監視的屬性定義特定的執行個體 (如果有的話)。  
  
-   **如果是計數器和值則發出警示**   
  
    警示的臨界值和產生警示的行為。 臨界值是一個數值。 此行為是下列其中一項：低於  、變成等於  或高於在 [值] 中指定的數值  。 [值]  是一個描述效能行況計數器的數值。 例如，若要設定警示在效能物件 **SQLServer:Locks** 的 **Lock Wait Time** 超過 30 分鐘時產生，您就必須選擇 [高於]  ，並指定 30 為 [值]  。  
  
    至於另一個範例，您可以指定效能物件 **SQLServer:Transactions** 在 **tempdb** 中的可用空間低於 1000 KB 時發出警示。 若要進行此設定，您必須選擇計數器 **Free space in tempdb (KB)** 、低於  ，並在 [值]  中指定 **1000**。  
  
    > [!NOTE]  
    > 效能資料是定期取樣的，因此在到達臨界值與發出效能警示之間可能會有一點延遲 (幾秒鐘)。  
  
## <a name="selecting-a-wmi-event"></a>選取 WMI 事件  
您可以指定一個為回應特定 WMI 事件而產生的警示。 若要選取 WMI 事件，您必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 [一般]  頁面上定義 [新增警示]  或 [警示屬性]  對話方塊中的下列項目：  
  
-   **Namespace**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會對可用的 WMI 命名空間註冊為 WMI 用戶端，以進行事件查詢。  
  
-   **查詢**  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會使用可用的 Windows Management Instrumentation 查詢語言 (WQL) 陳述式來識別特定的事件。  
  
以下是一般工作的連結：  
  
**若要以訊息編號為基礎建立警示**  
  
-   [Transact-SQL](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**若要以嚴重性層級為基礎建立警示**  
  
-   [Transact-SQL](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**若要根據 WMI 事件建立警示**  
  
-   [Transact-SQL](../../ssms/agent/create-a-wmi-event-alert.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**若要定義對警示的回應**  
  
-   [Transact-SQL](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
**若要建立使用者自訂的事件錯誤訊息**  
  
-   [Transact-SQL](https://msdn.microsoft.com/54746d30-f944-40e5-a707-f2d9be0fb9eb)  
  
**若要修改使用者自訂的事件錯誤訊息**  
  
-   [Transact-SQL](https://msdn.microsoft.com/1b28f280-8ef9-48e9-bd99-ec14d79abaca)  
  
**若要刪除使用者自訂的事件錯誤訊息**  
  
-   [Transact-SQL](https://msdn.microsoft.com/17287a15-cdde-43d1-bb18-9f920bc15db8)  
  
**若要停用或重新啟動警示**  
  
-   [Transact-SQL](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
## <a name="see-also"></a>另請參閱  
[sp_update_alert (Transact-SQL)](https://msdn.microsoft.com/bcd731b1-3c4e-4086-b58a-af7a3af904ad)  
  
