---
title: DROP EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL RESOURCE POOL
- DROP_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL RESOURCE POOL statement
ms.assetid: e2fa01bd-96ff-4ea9-bb08-6cb6b6adf68c
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7e4137d61fcb223f4fa4fc943314ecaa50965c51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690256"
---
# <a name="drop-external-resource-pool-transact-sql"></a>DROP EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  刪除 Resource Governor 用來定義外部處理序資源的外部資源集區。 若是 R 服務，外部集區會掌管 `rterm.exe`、`BxlServer.exe` 及其衍生的其他處理序。 外部資源集區是使用 [CREATE EXTERNAL RESOURCE POOL & #40;TRANSACT-SQL & #41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) 建立的，並使用 [ALTER EXTERNAL RESOURCE POOL & #40;TRANSACT-SQL & #41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) 加以修改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
  
```  
DROP EXTERNAL RESOURCE POOL pool_name  
```  
  
## <a name="arguments"></a>引數  
 *pool_name*  
 要刪除的外部資源集區名稱。  
  
## <a name="remarks"></a>Remarks  
 如果外部資源集區包含工作負載群組，您就無法將其卸除。  
  
 您無法卸除資源管理員的預設或內部集區。  
  
 重新設定會執行 n  
  
 當您要執行 DDL 陳述式時，建議您先熟悉資源管理員的狀態。 如需詳細資訊，請參閱 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)。  
  
## <a name="permissions"></a>[權限]  
 需要 `CONTROL SERVER` 權限。  
  
## <a name="examples"></a>範例  
 下列範例會卸除名稱為 `ex_pool` 的外部資源集區。  
  
```  
DROP EXTERNAL RESOURCE POOL ex_pool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [啟用外部指令碼伺服器設定選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [SQL Server R Services 已知問題](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)  
  
  
