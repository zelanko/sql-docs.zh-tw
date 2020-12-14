---
description: 'sys.database_scoped_configurations (Transact-sql) '
title: sys.database_scoped_configurations (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
dev_langs:
- TSQL
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||= azure-sqldw-latest
ms.openlocfilehash: beb536c39db6dbee3bc2e0855de20282bc994fe4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404714"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>sys.database_scoped_configurations (Transact-sql) 

[!INCLUDE[tsql-appliesto-ss2016-asdb-addw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

每個設定都包含一個資料列。 

|資料行名稱|資料類型|描述|
|-----------------|---------------|-----------------|
|**configuration_id**|**int**|設定選項的識別碼。|
|**name**|**nvarchar(60)**|設定選項的名稱。 如需可能設定的詳細資訊，請參閱 [ALTER DATABASE 範圍設定 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|
|**value**|**sqlvariant**|針對主要複本設定此設定選項的值。|
|**value_for_secondary**|**sqlvariant**|針對次要複本設定此設定選項的值。|
|**is_value_default**|**bit** |指定設定的值是否為預設值。|

## <a name="permissions"></a><a name="Permissions"></a> 權限

需要 **public** 角色的成員資格。

## <a name="remarks"></a>備註

如果傳回 Null 做為 **value_for_secondary** 的值，這表示次要設定為 [主要]。
 
資料庫範圍組態設定會伴隨著資料庫。 這意謂著還原或附加指定的資料庫時，現有的組態設定會持續存留。

## <a name="see-also"></a>另請參閱

[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
