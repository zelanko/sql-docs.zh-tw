---
title: "陳述式 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d780aa463f6d4defe7dc727091863feabe7f338a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="transact-sql-statements"></a>Transact-SQL 陳述式
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

本參考主題摘要說明用於 TRANSACT-SQL (T-SQL) 陳述式的類別。 您可以尋找所有在左側導覽列的陳述式。

## <a name="backup-and-restore"></a>備份與還原
備份和還原陳述式提供的方式來建立備份，並且從備份還原。  如需詳細資訊，請參閱[備份和還原的概觀](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。

## <a name="data-definition-language"></a>資料定義語言
資料定義語言 (DDL) 陳述式會定義資料結構。 您可以使用這些陳述式來建立、 改變或卸除資料庫中的資料結構。
- ALTER
- 定序
- CREATE
- DROP
- 停用觸發程序
- ENABLE TRIGGER
- 重新命名
- UPDATE STATISTICS

## <a name="data-manipulation-language"></a>資料操作語言
資料操作語言 (DML) 會影響儲存在資料庫中的資訊。 您可以使用這些陳述式來插入、 更新和變更資料庫中的資料列。

- BULK INSERT
- DELETE
- INSERT
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>權限陳述式
權限陳述式會判斷哪些使用者和登入可以存取資料，並執行作業。 如需驗證和存取的詳細資訊，請參閱[資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## <a name="service-broker-statements"></a>Service Broker 陳述式
提供傳訊和佇列應用程式的原生支援的功能，Service Broker。 如需詳細資訊，請參閱[Service Broker](../../relational-databases/service-broker/event-notifications.md)。

## <a name="session-settings"></a>工作階段設定
SET 陳述式決定目前的工作階段控制代碼執行時間設定的方式。 如需概觀，請參閱[SET 陳述式](set-statements-transact-sql.md)。

