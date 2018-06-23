---
title: 包含檔案
description: 包含檔案
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: 842a7377bcd6bdcb649a78b2f31eb66de95bc5a3
ms.sourcegitcommit: a98ed7872afc055c65aa9697d571f8b300f6eeb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313394"
---
## <a name="specifying-application-intent"></a>指定應用程式意圖

關鍵字**ApplicationIntent**可以在連接字串中指定。 指派的值為**ReadWrite**或**ReadOnly**。 預設值是**ReadWrite**。

當**ApplicationIntent = ReadOnly**，用戶端在連接時要求讀取工作負載。 在連接時間和期間，伺服器強制執行目的**使用**資料庫陳述式。

**ApplicationIntent**關鍵字不適用於舊版唯讀資料庫。  


#### <a name="targets-of-readonly"></a>ReadOnly 的目標

當連線選擇**ReadOnly**，連線會指派給任何資料庫可能有下列特殊組態：

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 資料庫可以允許或不允許目標 Alwayson 資料庫上的讀取工作負載。 這項選擇使用控制**ALLOW_CONNECTIONS**子句**PRIMARY_ROLE**和**SECONDARY_ROLE** TRANSACT-SQL 陳述式。

- [地理複寫](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [讀取擴充](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

如果這些特殊的目標都無法使用，則會從讀取一般資料庫。

&nbsp;

**ApplicationIntent**關鍵字可讓*唯讀路由*。


## <a name="read-only-routing"></a>唯讀路由

唯讀路由功能可確保資料庫之唯讀複本的可用性。 若要啟用唯讀路由，所有下列適用於：

- 您必須連接到 AlwaysOn 可用性群組的可用性群組接聽程式。

- **ApplicationIntent** 連接字串關鍵字必須設為 **ReadOnly**。

- 可用性群組必須由資料庫管理員設定為啟用唯讀路由。

多個連線使用唯讀路由不是所有可能會連線至相同的唯讀複本。 資料庫同步處理的變更或伺服器路由組態的變更，可能會導致用戶端連接至不同的唯讀複本。 您可以確保所有唯讀要求連接至相同的唯讀複本。 確定根據此 sameness*不*傳遞對可用性群組接聽程式**伺服器**連接字串關鍵字。 請改為指定唯讀執行個體的名稱。

唯讀路由可能會超過連接到主要複本。 較長的等待會是因為唯讀路由先連接到主要複本，而接著會尋找最佳可用可讀取次要複本。 由於這些多個 staps，您應該增加您登入逾時為至少 30 秒。

