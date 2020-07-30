---
title: 陳述式 | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0fc44d29ca0b94f03fd94e89d5ba442f53fdf5da
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87392006"
---
# <a name="transact-sql-statements"></a>Transact-SQL 陳述式

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SQL 陳述式是不可部分完成的工作單位，而且不是完全成功就是完全失敗。 SQL 陳述式是一組指令，其中包含識別碼、參數、變數、名稱、資料類型，以及可成功編譯的 SQL 保留字。 如果 `BeginTransaction` 命令未指定交易的開始，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為 SQL 陳述式建立「隱含」交易。 如果陳述式成功，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 永遠都會認可隱含交易；如果命令失敗，則會復原隱含交易。  

有許多類型的陳述式。 也許最重要的是 [SELECT](../queries/select-transact-sql.md)，其可從資料庫中擷取資料列，並可讓您從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的一或多個資料表選取一或多個資料列或資料行。 此文章摘要說明用於 Transact-SQL (T-SQL) (除了 `SELECT` 陳述式之外) 的類別。 您可以在左側導覽中找到所有的陳述式。

## <a name="backup-and-restore"></a>備份與還原

BACKUP 及 RESTORE 陳述式可讓您建立備份並從備份進行還原。  如需詳細資訊，請參閱[備份與還原概觀](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。

## <a name="data-definition-language"></a>資料定義語言

支援的資料定義語言 (DDL) 陳述式可定義資料結構。 使用這些陳述式建立、改變或卸除資料庫的資料結構。 這些陳述式包括：

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
- 刪除
- Insert
- SELECT
- UPDATE
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>權限陳述式

權限陳述式會判斷哪些使用者和登入可以存取資料與執行作業。 如需驗證和存取的詳細資訊，請參閱[資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## <a name="service-broker-statements"></a>Service Broker 陳述式

Service Broker 是一種功能，可提供傳訊和查詢應用程式的原生支援。 如需詳細資訊，請參閱 [Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)。

## <a name="session-settings"></a>工作階段設定

SET 陳述式可決定目前工作階段處理執行時間設定的方式。 如需概觀，請參閱 [SET 陳述式](set-statements-transact-sql.md)。
