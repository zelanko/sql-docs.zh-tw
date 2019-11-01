---
title: database_scoped_configurations （Transact-sql） |Microsoft Docs
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
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da115c8d4cf48cfbcd6190c88a83bee4e61ae5a1
ms.sourcegitcommit: 27c267bf2a3cfaf2abcb5f3777534803bf4cffe5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240765"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>database_scoped_configurations （Transact-sql）

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

針對每個設定包含一個資料列。 

|資料行名稱|[名稱]|[描述]|
|-----------------|---------------|-----------------|
|**configuration_id**|**整數**|設定選項的識別碼。|
|**name**|**nvarchar(60)**|設定選項的名稱。 如需可能設定的詳細資訊，請參閱[ALTER DATABASE &#40;範圍設定 transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|
|**value**|**sqlvariant**|針對主要複本的這個設定選項所設定的值。|
|**value_for_secondary**|**sqlvariant**|次要複本的這個設定選項所設定的值。|
|**is_value_default**|**bit** |指定值是否設定為預設值。|

## <a name="Permissions"></a> Permissions

需要 **public** 角色的成員資格。

## <a name="remarks"></a>Remarks

當傳回 Null 做為**value_for_secondary**的值時，這表示次要複本設定為 PRIMARY。
 
資料庫範圍組態設定會伴隨著資料庫。 這意謂著還原或附加指定的資料庫時，現有的組態設定會持續存留。

## <a name="see-also"></a>請參閱

[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
