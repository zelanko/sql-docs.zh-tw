---
title: "使用 Stretch Database 設定相容的 SQL Server 功能 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8121ede-1aec-459b-b7b0-1408bb3e62fb
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e3a82010a06b505e22d9706c070f9bf4ce5d45d3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="configure-compatible-sql-server-features-with-stretch-database"></a>使用 Stretch Database 設定相容的 SQL Server 功能
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

採取簡單的步驟即可設定下列的 SQL Server 功能，以便使用 Stretch Database。
-   Always On
-   永遠加密
-   透明資料加密 (TDE)
-   時態表

## <a name="configure-always-on-with-stretch-database"></a>使用 Stretch Database 設定永遠開啟
如果您使用 Always On 搭配 Stretch Database，必須確定資料庫主要金鑰可用在次要複本。 Stretch Database 使用資料庫主要金鑰，來保護它用來連接遠端 Azure 資料庫的認證。

您設定 Always On 可用性群組之後，請在每個次要複本上執行預存程序 **sp_control_dbmasterkey_password** ，並提供啟用 Stretch 之資料庫的密碼。 如需詳細資訊和範例，請參閱 [sp_control_dbmasterkey_password](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)。 

## <a name="configure-always-encrypted-with-stretch-database"></a>使用 Stretch Database 設定永遠加密
如果您想要同時使用永遠加密和 Stretch Database，您必須在所選資料行上設定加密，然後才在資料表上啟用 Stretch Database。

如果您已在資料表上啟用 Stretch Database，而且您想要使用永遠加密資料行，您必須執行下列動作。
1.   在資料表上停用 Stretch Database，並從 Azure 帶回遠端資料。 如需詳細資訊，請參閱 [停用 Stretch Database 並帶回遠端資料](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)。
2.   在選取的資料行上，設定永遠加密。
3. 在資料表上重新啟用 Stretch Database。 如需詳細資訊，請參閱 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)。

## <a name="configure-transparent-data-encryption-tde-with-stretch-database"></a>使用 Stretch Database 設定透明資料加密 (TDE)

如果在本機資料庫上已啟用 TDE，它不會在 Stretch Database 遠端端點上自動啟用。 您必須記得先在資料庫上啟用 Stretch Database，然後才在遠端端點上啟用 TDE。

## <a name="configure-temporal-tables-with-stretch-database"></a>使用 Stretch Database 設定時態表
如果您使用時態表，您可以在歷程記錄資料表上啟用 Stretch Database，但不能在目前的資料表。
-   如需搭配使用時態表與 Stretch Database 的指引，請參閱 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)。
-   若要使用滑動視窗篩選要從歷程記錄資料表移轉的資料列，請參閱 [使用篩選函數選取要移轉的資料列](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)。
-   如果時態性記錄資料表已經過記憶體最佳化，您就無法在該處啟用 Stretch Database。 記憶體最佳化資料表未受支援。
