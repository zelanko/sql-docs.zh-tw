---
title: 陳述式 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
caps.latest.revision: 7
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ecd72419630de8754a46f29150be1ead79a2140f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43062590"
---
# <a name="transact-sql-statements"></a>Transact-SQL 陳述式
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

本參考主題摘要說明用於 Transact-SQL (T-SQL) 陳述式的類別。 您可以在左側導覽中找到所有的陳述式。

## <a name="backup-and-restore"></a>備份與還原
BACKUP 及 RESTORE 陳述式可讓您建立備份並從備份進行還原。  如需詳細資訊，請參閱[備份與還原概觀](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。

## <a name="data-definition-language"></a>資料定義語言
支援的資料定義語言 (DDL) 陳述式可定義資料結構。 使用這些陳述式建立、改變或卸除資料庫的資料結構。
- ALTER
- 定序
- CREATE
- DROP
- DISABLE TRIGGER
- ENABLE TRIGGER
- RENAME
- UPDATE STATISTICS

## <a name="data-manipulation-language"></a>資料操作語言
資料操作語言 (DML) 會影響儲存在資料庫中的資訊。 您可以使用這些陳述式來插入、更新和變更資料庫中的資料列。

- BULK INSERT
- Delete
- Insert
- UPDATE
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>權限陳述式
權限陳述式會判斷哪些使用者和登入可以存取資料與執行作業。 如需驗證和存取的詳細資訊，請參閱[資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## <a name="service-broker-statements"></a>Service Broker 陳述式
Service Broker 是一種功能，可提供傳訊和查詢應用程式的原生支援。 如需詳細資訊，請參閱 [Service Broker](../../relational-databases/service-broker/event-notifications.md)。

## <a name="session-settings"></a>工作階段設定
SET 陳述式可決定目前工作階段處理執行時間設定的方式。 如需概觀，請參閱 [SET 陳述式](set-statements-transact-sql.md)。
