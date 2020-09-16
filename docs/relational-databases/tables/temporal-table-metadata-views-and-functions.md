---
description: 暫存資料表中繼資料檢視和函數
title: 暫存資料表中繼資料檢視和函式 | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: e5d23ec9-7d18-40f6-add4-bea13132d0b9
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d71f195f6432a5d27598d7861526f2a6475307c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537823"
---
# <a name="temporal-table-metadata-views-and-functions"></a>暫存資料表中繼資料檢視和函數


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 包括數個 Metabase 檢視及函數，可讓系統管理員擷取暫存資料表的相關資訊。

暫存資料表相關資訊會顯示在下列中繼資料檢視中︰

- [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)
- [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)
- [sys.periods &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-periods-transact-sql.md)

 暫存資料表相關資訊會顯示在下列中繼資料函式中︰

- [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)

- [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)

- [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)

## <a name="next-steps"></a>後續步驟

- [時態表](../../relational-databases/tables/temporal-tables.md)
- [開始使用系統建立版本的時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [對時態表進行資料分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [時態表考量與限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [時態表安全性](../../relational-databases/tables/temporal-table-security.md)
- [管理系統設定版本時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
