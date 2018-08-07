---
title: PolyBase 連接組態 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PolyBase
ms.assetid: 82252e4f-b1d0-49e5-aa0b-3624aade2add
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4f67ce40623a69dfaa7fbfc0c6f64486a8a25bbc
ms.sourcegitcommit: d9b7625322a2c7444ed25ca311d63fe70eb6fa0a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2018
ms.locfileid: "39509227"
---
# <a name="polybase-connectivity-configuration-transact-sql"></a>PolyBase 連接組態 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]

  顯示或變更適用於 PolyBase Hadoop 和 Azure Blob 儲存體連接的全域組態設定。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
--List all of the configuration options  
sp_configure  
[;]  
  
--Configure Hadoop connectivity  
sp_configure [ @configname = ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ **@configname=** ] **'***option_name***'**  
 這是組態選項的名稱。 *option_name* is **varchar(35)**，預設值為 NULL。 若未指定，就會傳回完整的選項清單。  
  
 [ **@configvalue=** ] **'***value***'**  
 這是新的組態設定。 *value* 是 **int**，預設值是 NULL。 最大值會隨著個別選項而不同。  
  
 **'hadoop connectivity'**  
 針對所有從 PolyBase 到 Hadoop 叢集或 Azure Blob 儲存體 (WASB) 的連接，指定此類型的 Hadoop 資料來源。 需要此設定，才能建立外部資料表的外部資料來源。 如需詳細資訊，請參閱 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)。  
  
 這些是 Hadoop 連接性設定及其對應的支援 Hadoop 資料來源。 一次只能有一個設定生效。 選項 1、 4 和 7 可讓多個類型的外部資料來源能夠在伺服器上的所有工作階段之間建立和使用。  
  
-   選項 0︰停用 Hadoop 連接  
  
-   選項 1：Windows Server 上的 Hortonworks HDP 1.3  
  
-   選項 1：Azure Blob 儲存體 (WASB[S])  
  
-   選項 2：Linux 上的 Hortonworks HDP 1.3  
  
-   選項 3：Linux 上的 Cloudera CDH 4.3  
  
-   選項 4：Windows Server 上的 Hortonworks HDP 2.0  
  
-   選項 4：Azure Blob 儲存體 (WASB[S])  
  
-   選項 5：Linux 上的 Hortonworks HDP 2.0  
  
-   選項 6：Linux 上的 Cloudera 5.1、5.2、5.3、5.4、5.5、5.9、5.10、5.11、5.12 和 5.13  
  
-   選項 7：Linux 上的 Hortonworks 2.1、2.2、2.3、2.4、2.5 和 2.6  
  
-   選項 7：Windows Server 上的 Hortonworks 2.1、2.2 和 2.3  
  
-   選項 7：Azure Blob 儲存體 (WASB[S])  
  
 **RECONFIGURE**  
 更新執行值 (run_value) 以符合組態值 (config_value)。 如需 run_value 和 config_value 的定義，請參閱 [結果集](#ResultSets) 。 sp_configure 所設定的新組態值不會在 RECONFIGURE 陳述式設定執行值之前生效。  
  
 執行 RECONFIGURE 之後，您必須停止並重新啟動 SQL Server 服務。 請注意，在停止 SQL Server 服務時，其他兩個 PolyBase 引擎和資料移動服務將會自動停止。 重新啟動 SQL Server 引擎服務之後，請再次重新啟動這兩個服務 (它們不會自動啟動)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
##  <a name="ResultSets"></a> 結果集  
 如果執行時未使用任何參數， **sp_configure** 就會傳回含有五個資料行的結果集。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|組態選項的名稱。|  
|**minimum**|**int**|組態選項的最小值。|  
|**maximum**|**int**|組態選項的最大值。|  
|**config_value**|**int**|使用 **sp_configure**設定的值。|  
|**run_value**|**int**|PolyBase 目前使用的值。 這個值是藉由執行 RECONFIGURE 來設定。<br /><br /> 除非正在變更值，否則 **config_value** 和 **run_value** 通常會一樣。<br /><br /> 如果正在進行重新設定，就可能需要重新啟動，才能讓這個執行值正確。|  
  
## <a name="general-remarks"></a>一般備註  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，執行 RECONFIGURE 之後，若要讓 'hadoop connectivity' 的值生效，您需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
在 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中，執行 RECONFIGURE 之後，若要讓 'hadoop connectivity' 的值生效，您需要重新啟動 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 區域。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 在明確或隱含的交易中，不允許使用 RECONFIGURE。  
  
## <a name="permissions"></a>[權限]  
 所有的使用者都可以執行 **sp_configure** 且不含參數或搭配 @configname 參數。  
  
 需要 **系統管理員** 固定伺服器角色中的 **ALTER SETTINGS** 伺服器層級權限或成員資格，來變更組態值或執行 RECONFIGURE。  
  
## <a name="examples"></a>範例  
  
### <a name="a-list-all-available-configuration-settings"></a>A. 列出所有可用的組態設定  
 下列範例示範如何列出所有組態選項。  
  
```  
EXEC sp_configure;  
```  
  
 結果會傳回選項名稱，後面接著選項的最小值和最大值。 **config_value** 是重新設定完成時，SQL 或 PolyBase 將使用的值。 **run_value** 是目前正在使用的值。 除非正在變更值，否則 **config_value** 和 **run_value** 通常會一樣。  
  
### <a name="b-list-the-configuration-settings-for-one-configuration-name"></a>B. 列出某一個組態名稱的組態設定  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="c-set-hadoop-connectivity"></a>C. 設定 Hadoop 連接  
 此範例會將 PolyBase 設定選項 7。 此選項將允許 PolyBase 在 Linux 和 Windows Server 的 Hortonworks 2.1、2.2 和 2.3 上，以及 Azure Blob 儲存體上，建立和使用外部資料表。 例如，SQL 有 30 個外部資料表，其中 7 個會參考 Linux 的 Hortonworks 2.1 上的資料、4 個會參考 Linux 的 Hortonworks 2.2 上的資料、7 個會參考 Linux 的 Hortonworks 2.3 上的資料，而其他的 12 個會參考 Azure Blob 儲存體。  
  
```  
--Configure external tables to reference data on Hortonworks 2.1, 2.2, and 2.3 on Linux, and Azure blob storage  
  
sp_configure @configname = 'hadoop connectivity', @configvalue = 7;  
GO  
  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
