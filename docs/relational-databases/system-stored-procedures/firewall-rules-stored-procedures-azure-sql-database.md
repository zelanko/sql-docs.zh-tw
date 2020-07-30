---
title: 防火牆規則預存程序
titleSuffix: Azure SQL Database
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- firewall rules stored procedures
- firewall_rules, setting
- firewall_rules, Azure SQL Database
- firewall systems, Azure SQL Database
ms.assetid: 3d4c2585-00de-46b5-8eee-0efb71cb3aea
author: VanMSFT
ms.author: vanto
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: d06646127c59dca8e72f061b049cabb42f8073ab
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246687"
---
# <a name="firewall-rules-stored-procedures-azure-sql-database"></a>防火牆規則預存程式（Azure SQL Database）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  此節包含下列設定或刪除防火牆規則的預存程序。 [!INCLUDE[tsql_md](../../includes/tsql-md.md)]防火牆規則可以與和搭配 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 使用 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 。 如需詳細資訊，請參閱[設定 Azure SQL Database 防火牆規則-總覽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)。

:::row:::
    :::column:::
        [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)
    :::column-end:::
    :::column:::
        [sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)
    :::column-end:::
    :::column:::
        [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)
    :::column-end:::
:::row-end:::

&nbsp;
  
針對 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，請使用視窗防火牆規則。 如需詳細資訊，請參閱 [設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。   
  


