---
title: sys.configurations （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7986fc4286cf681507a80a72f2f308b6a96f413a
ms.sourcegitcommit: 9921501952147b9ce3e85a1712495d5b3eb13e5b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84215852"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對系統中每個伺服器範圍組態選項值，各包含一個資料列。  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|組態值的唯一識別碼。|  
|**name**|**nvarchar(35)**|組態選項的名稱。|  
|**value**|**sql_variant**|針對這個選項所設定的值。|  
|**至少**|**sql_variant**|組態選項的最小值。|  
|**高**|**sql_variant**|組態選項的最大值。|  
|**value_in_use**|**sql_variant**|這個選項目前有效的執行值。|  
|**描述**|**nvarchar(255)**|組態選項的描述。|  
|**is_dynamic**|**bit**|1 = 在執行 RECONFIGURE 陳述式時的有效變數。|  
|**is_advanced**|**bit**|1 = 只有在已設定**show advancedoption**時，才會顯示變數。|  
  
 ## <a name="remarks"></a>備註
  如需所有伺服器設定選項的清單，請參閱[伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
> [!NOTE]  
>  如需資料庫層級的設定選項，請參閱[ALTER DATABASE 範圍設定 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 若要設定軟體 NUMA，請參閱[軟體 numa &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
 
[sys.configurations 目錄] 視圖可用來決定 config_value （[值] 資料行）、[run_value] （[value_in_use] 資料行），以及 [設定] 選項是否為 [動態] （不需要重新開機伺服器引擎或 is_dynamic 資料行）。

> [!NOTE]
> Sp_configure 結果集內的 config_value 相當於**sys.config的 urations 值**資料行。 **Run_value**等同于**sys.configurations. value_in_use**資料行。

下列查詢可以用來判斷是否有任何設定的值尚未安裝：

```SQL
select * from sys.configurations where value != value_in_use
```

如果此值等於您所做之設定選項的變更，但**value_in_use**不相同，可能是重新設定命令未執行或失敗，或伺服器引擎必須重新開機。

有一些設定選項的值和 value_in_use 可能不相同，而且這是預期的行為。 例如：

「最大伺服器記憶體（MB）」-預設設定的值為0會顯示為 value_in_use = 2147483647 "min server memory （MB）"-預設設定的值為0可能會顯示為 value_in_use = 8 （32位）或16（64位）。 

在某些情況下， **value_in_use**將會是0。 在此情況下，"true" **value_in_use**是8（32位）或16（64位）

**Is_dynamic**資料行可以用來判斷設定選項是否需要重新開機。 is_dynamic = 1 表示當執行重新設定（T-sql）命令時，新值會立即生效（在某些情況下，伺服器引擎可能無法立即評估新值，但在正常執行過程中會這麼做）。 is_dynamic = 0 表示已變更的設定值在伺服器重新開機後才會生效，即使執行了重新設定（T-sql）命令也一樣。

對於非動態的設定選項，無法分辨是否已執行重新設定（T-sql）命令來執行安裝設定變更的第一個步驟。 重新開機 SQL Server 以安裝設定變更之前，請執行重新設定（T-sql）命令，以確保所有設定變更都會在 SQL Server 重新開機之後生效。 
 
 
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的伺服器範圍設定目錄檢視](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
