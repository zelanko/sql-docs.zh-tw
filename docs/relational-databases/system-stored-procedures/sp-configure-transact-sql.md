---
title: sp_configure (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 23b75beb0782fc0a13155d12890cbe3a620e1733
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530240"
---
# <a name="spconfigure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-pdw-md.md)]

  顯示或變更目前伺服器的全域組態設定。

> [!NOTE]  
>  如需資料庫層級組態選項，請參閱[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 若要設定軟體 NUMA，請參閱[NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
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
`[ @configname = ] 'option_name'` 是組態選項的名稱。 *option_name* is **varchar(35)**，預設值為 NULL。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會識別任何屬於組態名稱一部分的唯一字串。 若未指定，就會傳回完整的選項清單。  
  
 如需有關可用組態選項及其設定的資訊，請參閱[伺服器組態選項&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
`[ @configvalue = ] 'value'` 這新的組態設定。 *value* 是 **int**，預設值是 NULL。 最大值會隨著個別選項而不同。  
  
 若要查看每個選項的最大值，請參閱**最大**資料行**sys.configurations**目錄檢視。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 不使用參數執行時**sp_configure**傳回含有五個資料行的結果集與訂單依照字母的遞增順序 選項下, 表所示。  
  
 值**config_value**並**run_value**不會自動相等。 使用更新的組態設定之後**sp_configure**，系統管理員必須使用 RECONFIGURE 或 RECONFIGURE WITH OVERRIDE，更新執行中的組態值。 如需詳細資訊，請參閱＜備註＞一節。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|組態選項的名稱。|  
|**minimum**|**int**|組態選項的最小值。|  
|**maximum**|**int**|組態選項的最大值。|  
|**config_value**|**int**|[設定] 選項已設定使用的值**sp_configure** (值**sys.configurations.value**)。 如需這些選項的詳細資訊，請參閱[伺服器組態選項&#40;SQL Server&#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md)並[sys.configurations &#40;-&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)。|  
|**run_value**|**int**|目前執行中的組態選項值 (值**sys.configurations.value_in_use**)。<br /><br /> 如需詳細資訊，請參閱 < [sys.configurations &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)。|  
  
## <a name="remarks"></a>備註  
 使用**sp_configure**來顯示或變更伺服器層級設定。 若要變更資料庫層級的設定，請使用 ALTER DATABASE。 若要變更只影響目前使用者工作階段的設定，請使用 SET 陳述式。  
  
## <a name="updating-the-running-configuration-value"></a>更新執行中的組態值  
 當您指定的新*值*for*選項*，結果集會顯示此值**config_value**資料行。 一開始，這個值會不同於中的值**run_value**資料行，顯示目前正在執行的組態值。 若要執行的設定值，在**run_value**  欄中，系統管理員必須執行 RECONFIGURE 或 RECONFIGURE WITH OVERRIDE。  
  
 RECONFIGURE 和 RECONFIGURE WITH OVERRIDE 都會使用每個組態選項。 不過，基本 RECONFIGURE 陳述式會拒絕在合理範圍之外或可能造成選項衝突的任何選項值。 比方說，RECONFIGURE 就會產生錯誤如果**復原間隔**值大於 60 分鐘的時間或者**親和性遮罩**值與重疊**affinity I/O mask**值。 相對地，RECONFIGURE WITH OVERRIDE 會接受任何資料類型正確的選項值，且會強迫利用指定的值來重設組態。  
  
> [!CAUTION]  
>  不恰當的選項值可能會對伺服器執行個體的組態產生負面的影響。 當使用 RECONFIGURE WITH OVERRIDE 時，請特別小心。  
  
 RECONFIGURE 陳述式會動態更新某些選項；其他選項則需要伺服器停止再重新啟動。 例如，**最小伺服器記憶體**並**最大伺服器記憶體**伺服器記憶體選項會動態更新[!INCLUDE[ssDE](../../includes/ssde-md.md)]; 因此，您可以變更它們而不需要重新啟動伺服器。 相反地，重新設定的執行中的值**填滿因數**選項需要重新啟動[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
 執行之後重新設定組態選項，您可以看到是否選項已動態更新執行**sp_configure'***option_name***'**。 中的值**run_value**並**config_value**資料行應該符合動態更新的選項。 您也可以檢查以查看哪些選項是動態的藉由查看**sys.configurations**資料行**sys.configurations**目錄檢視。  
  
> [!NOTE]  
>  如果指定*值*太高的選項，如**run_value**資料行反映，[!INCLUDE[ssDE](../../includes/ssde-md.md)]已預設為動態記憶體，而不是使用不是有效的設定。  
  
 如需詳細資訊，請參閱 < [RECONFIGURE &#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)。  
  
## <a name="advanced-options"></a>[進階選項]  
 部分組態選項，例如**親和性遮罩**並**復原間隔**，指定為進階選項。 依預設，這些選項無法檢視和變更。 若要讓它們，請設定**ShowAdvancedOptions**組態選項設為 1。  
  
 如需有關組態選項和其設定的詳細資訊，請參閱[伺服器組態選項&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 若要執行**sp_configure**兩個參數來變更組態選項或執行 RECONFIGURE 陳述式，您必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. 列出進階組態選項  
 下列範例會顯示如何設定和列出所有組態選項。 首先將 `show advanced option` 設為 `1` 來顯示進階組態選項。 變更好這個選項之後，執行不含任何參數的 `sp_configure` 會顯示所有組態選項。  
  
```  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 以下是訊息：「 組態選項 'show advanced 的 options' 從 0 變更為 1。 請執行 RECONFIGURE 陳述式來安裝。」  
  
 執行 `RECONFIGURE` 和顯示所有組態選項：  
  
```  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>B. 變更組態選項  
 下列範例將系統 `recovery interval` 設為 `3` 分鐘。  
  
```  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>C. 列出所有可用的組態設定  
 下列範例示範如何列出所有組態選項。  
  
```  
EXEC sp_configure;  
```  
  
 結果會傳回選項名稱，後面接著選項的最小值和最大值。 **Config_value**的值，[!INCLUDE[ssDW](../../includes/ssdw-md.md)]重新設定完成時，會使用。 **run_value** 是目前正在使用的值。 除非正在變更值，否則 **config_value** 和 **run_value** 通常會一樣。  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. 列出某一個組態名稱的組態設定  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. 設定 Hadoop 連接  
 設定 Hadoop 連接需要幾個步驟，除了執行 sp_configure。 如需完整的程序，請參閱[CREATE EXTERNAL DATA SOURCE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [軟體 NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
