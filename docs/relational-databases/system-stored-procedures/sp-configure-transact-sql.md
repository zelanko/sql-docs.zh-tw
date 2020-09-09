---
description: sp_configure (Transact-SQL)
title: sp_configure (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: dd9ba41579e8d1c0bac76bb634e9074bf9e5c670
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536626"
---
# <a name="sp_configure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-pdw-md.md)]

  顯示或變更目前伺服器的全域組態設定。

> [!NOTE]  
> 如需資料庫層級的設定選項，請參閱 [ALTER DATABASE 範圍設定 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 若要設定軟體 NUMA，請參閱 [軟體 numa &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Syntax for SQL Server  
  
sp_configure [ [ @configname = ] 'option_name'   
    [ , [ @configvalue = ] 'value' ] ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- List all of the configuration options  
sp_configure  
[;]  
  
-- Configure Hadoop connectivity  
sp_configure [ @configname= ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>引數  
`[ @configname = ] 'option_name'` 這是設定選項的名稱。 *option_name* is **varchar(35)** ，預設值為 NULL。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會識別任何屬於組態名稱一部分的唯一字串。 若未指定，就會傳回完整的選項清單。  
  
 如需可用設定選項及其設定的詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
`[ @configvalue = ] 'value'` 是新的設定。 *value* 是 **int**，預設值是 NULL。 最大值會隨著個別選項而不同。  
  
 若要查看每個選項的最大值，請參閱**sys.configurations**目錄檢視的 [**最大**值] 資料行。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 如果執行時沒有參數， **sp_configure** 會傳回含有五個數據行的結果集，並以遞增順序排序選項，如下表所示。  
  
 **Config_value**和**run_value**的值不會自動相等。 使用 **sp_configure**更新設定設定之後，系統管理員必須使用 [重新設定] 或 [重新設定為覆寫] 來更新執行中的設定值。 如需詳細資訊，請參閱＜備註＞一節。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|組態選項的名稱。|  
|**minimum**|**int**|組態選項的最小值。|  
|**maximum**|**int**|組態選項的最大值。|  
|**config_value**|**int**|設定選項的設定值，這個值會在**sys.configurations**中使用**sp_configure** (值) 。 如需這些選項的詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md) 和 [sys.configurations &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)。|  
|**run_value**|**int**|目前正在執行設定選項的值 (sys.configurations 中的值 ** 。 value_in_use**) 。<br /><br /> 如需詳細資訊，請參閱 [sys.configurations &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)。|  
  
## <a name="remarks"></a>備註  
 使用 **sp_configure** 來顯示或變更伺服器層級設定。 若要變更資料庫層級的設定，請使用 ALTER DATABASE。 若要變更只影響目前使用者工作階段的設定，請使用 SET 陳述式。  
  
### [!INCLUDE [ssbigdataclusters-ss-nover](../../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE [big-data-clusters-master-instance-ha-endpoint-requirement](../../includes/big-data-clusters-master-instance-ha-endpoint-requirement.md)]

## <a name="updating-the-running-configuration-value"></a>更新執行中的組態值  
 當您指定*選項*的新*值*時，結果集會在**config_value**資料行中顯示這個值。 此值一開始與 **run_value** 資料行中的值不同，它會顯示目前正在執行的設定值。 若要更新 **run_value** 資料行中的執行中設定值，系統管理員必須執行 [重新設定] 或 [重新設定為覆寫]。  
  
 RECONFIGURE 和 RECONFIGURE WITH OVERRIDE 都會使用每個組態選項。 不過，基本 RECONFIGURE 陳述式會拒絕在合理範圍之外或可能造成選項衝突的任何選項值。 例如，如果復原 **間隔** 值大於60分鐘或 **親** 和性遮罩值與 **親和性 i/o 遮罩** 值重迭，則重新設定會產生錯誤。 相對地，RECONFIGURE WITH OVERRIDE 會接受任何資料類型正確的選項值，且會強迫利用指定的值來重設組態。  
  
> [!CAUTION]  
> 不恰當的選項值可能會對伺服器執行個體的組態產生負面的影響。 當使用 RECONFIGURE WITH OVERRIDE 時，請特別小心。  
  
 RECONFIGURE 陳述式會動態更新某些選項；其他選項則需要伺服器停止再重新啟動。 例如，[ **最小伺服器記憶體** ] 和 [ **最大伺服器** 記憶體] 伺服器記憶體選項會在中動態更新， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 因此您可以變更它們，而不需要重新開機伺服器。 相反地，重新設定 **填滿因數** 選項的執行值，需要重新開機 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。  
  
 在設定選項上執行重新設定之後，您可以藉由執行 **sp_configure '***option_name***'**，來查看選項是否已動態更新。 在 [ **run_value** ] 和 [ **config_value** ] 資料行中的值應該符合動態更新的選項。 您也可以查看**sys.configurations**類別目錄檢視的 [ **is_dynamic** ] 資料行，以查看哪些選項是動態的。  
 
 這項變更也會寫入 SQL Server 錯誤記錄檔中。
  
> [!NOTE]  
>  如果指定的 *值* 對某個選項而言太高， **run_value** 資料行會反映預設為動態記憶體的事實，而不是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用不正確設定。  
  
 如需詳細資訊，請參閱 [重新設定 &#40;transact-sql&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)。  
  
## <a name="advanced-options"></a>進階選項  
 某些設定選項（例如 **親和性遮罩** 和復原 **間隔**）會指定為 advanced options。 依預設，這些選項無法檢視和變更。 若要使其可供使用，請將 **設定 showadvancedoptions** 設定選項設定為1。  
  
 如需設定選項及其設定的詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
## <a name="permissions"></a>權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 若要使用兩個參數來執行 **sp_configure** 來變更設定選項或執行重新設定語句，您必須授與 ALTER SETTINGS 伺服器層級許可權。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. 列出進階組態選項  
 下列範例會顯示如何設定和列出所有組態選項。 首先將 `show advanced option` 設為 `1` 來顯示進階組態選項。 變更好這個選項之後，執行不含任何參數的 `sp_configure` 會顯示所有組態選項。  
  
```sql  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 訊息如下：「組態選項 'show advanced options' 從 0 變更為 1。 請執行 RECONFIGURE 陳述式來安裝。」  
  
 執行 `RECONFIGURE` 和顯示所有組態選項：  
  
```sql  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>B. 變更組態選項  
 下列範例將系統 `recovery interval` 設為 `3` 分鐘。  
  
```sql  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-sspdw"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>C. 列出所有可用的組態設定  
 下列範例示範如何列出所有組態選項。  
  
```sql  
EXEC sp_configure;  
```  
  
 結果會傳回選項名稱，後面接著選項的最小值和最大值。 **Config_value**是重新設定 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 完成時將使用的值。 **run_value** 是目前正在使用的值。 除非正在變更值，否則 **config_value** 和 **run_value** 通常會一樣。  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. 列出某一個組態名稱的組態設定  
  
```sql  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. 設定 Hadoop 連接  
 除了執行 sp_configure 之外，設定 Hadoop 連線還需要更多步驟。 如需完整的程式，請參閱 [CREATE EXTERNAL DATA SOURCE &#40;transact-sql&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [軟體 NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
