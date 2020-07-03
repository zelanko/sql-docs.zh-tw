---
title: sp_serveroption （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_serveroption_TSQL
- sp_serveroption
dev_langs:
- TSQL
helpviewer_keywords:
- 7343 (Database Engine error)
- sp_serveroption
ms.assetid: 47d04a2b-dbf0-4f15-bd9b-81a2efc48131
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ddaed4baff5685f4ebf7bf4083c9264c895cdd32
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893210"
---
# <a name="sp_serveroption-transact-sql"></a>sp_serveroption (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  設定遠端伺服器和連結伺服器的伺服器選項。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_serveroption [@server = ] 'server'   
      ,[@optname = ] 'option_name'       
      ,[@optvalue = ] 'option_value' ;  
```  
  
## <a name="arguments"></a>引數  
`[ @server = ] 'server'`這是要設定選項的伺服器名稱。 *server* 是 **sysname**，沒有預設值。  
  
`[ @optname = ] 'option_name'`這是針對指定伺服器設定的選項。 *option_name*為**Varchar （** 35 **）**，沒有預設值。 *option_name*可以是下列任何一個值。  
  
|值|說明|  
|-----------|-----------------|  
|**定序相容**|影響針對連結伺服器的分散式查詢執行。 如果此選項設定為**true**，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會假設連結伺服器中的所有字元都與本機伺服器相容，與字元集和定序順序（或排序次序）有關。 這會使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠將字元資料行的比較傳給提供者。 如果未設定這個選項， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一律會在本機環境中評估字元資料行的比較。<br /><br /> 只有在確定對應於連結伺服器的資料來源與本機伺服器的字元集和排序順序相同時，才應該設定這個選項。|  
|**定序名稱**|如果 [**使用遠端定序]** 為**true** ，而且資料來源不是資料來源，則指定遠端資料源所使用的定序名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這個名稱必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所支援的定序之一。<br /><br /> 當存取不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但其定序卻符合某項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序的 OLE DB 資料來源時，請使用這個選項。<br /><br /> 連結伺服器必須支援供這部伺服器的所有資料行使用的單一定序。 如果連結伺服器支援單一資料來源內的多重定序，或無法確定連結伺服器的定序是否符合某項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序時，請勿設定這個選項。|  
|**連接逾時**|連接到連結伺服器的超時 valuein 秒數。<br /><br /> 如果是**0**，請使用**sp_configure**預設值。|  
|**資料存取**|啟用和停用連結伺服器的分散式查詢存取。 只能用於透過**sp_addlinkedserver**新增的**sys. server**專案。|  
|**dist**|散發者。|  
|**lazy schema validation**|判斷是否將檢查遠端資料表的結構描述。<br /><br /> 若**為 true**，則在查詢的開頭略過遠端資料表的架構檢查。|  
|**pub**|簽發者。|  
|**查詢超時**|針對連結伺服器進行查詢的逾時值。<br /><br /> 如果是**0**，請使用**sp_configure**預設值。|  
|**4**|從給定伺服器啟用 RPC。|  
|**rpc 輸出**|啟用指向給定伺服器的 RPC。|  
|**sub**|訂閱者。|  
|**系統**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**使用遠端定序**|決定將使用遠端資料行或本機伺服器的定序。<br /><br /> 若為**true**，則會使用遠端資料行的定序做為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源，而定**序名稱**中所指定的定序則用於非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源。<br /><br /> 若**為 false**，分散式查詢一律會使用本機伺服器的預設定序，而定**序名稱**和遠端資料行的定序則會被忽略。 預設值為 **false**。 （ **False**值與7.0 中使用的定序語義相容 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ）。|  
|**remote proc transaction promotion**|使用此選項，透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 交易，保護伺服器對伺服器程序的動作。 當此選項為 TRUE (或 ON) 時，呼叫遠端預存程序就會啟動分散式交易，而且會利用 MS DTC 來編列這項交易。 發出遠端預存程序呼叫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是交易發起者，它會控制交易的完成。 當發出連接的後續 COMMIT TRANSACTION 或 ROLLBACK TRANSACTION 陳述式時，負責控制的執行個體會要求 MS DTC 跨越所涉及的各部電腦來管理分散式交易的完成。<br /><br /> 在啟動 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散式交易之後，會向已定義為連結伺服器的其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體發出遠端預存程序呼叫。 所有連結伺服器都會編列在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散式交易中，MS DTC 會確保已針對每部連結伺服器來完成交易。<br /><br /> 如果此選項設定為 FALSE (或 OFF)，在連結伺服器上呼叫遠端預存程序時，本機交易將不會升級為分散式交易。<br /><br /> 如果在進行伺服器對伺服器的程序呼叫之前，此交易已經是分散式交易，則此選項不會有任何影響。 針對連結伺服器執行的程序呼叫將會在相同的分散式交易之下執行。<br /><br /> 如果在進行伺服器對伺服器的程序呼叫之前，連接中沒有任何使用中的交易，則此選項不會有任何影響。 然後此程序會在沒有使用中交易的情況下對連結伺服器執行。<br /><br /> 這個選項的預設值是 TRUE (或 ON)。|  
  
`[ @optvalue = ] 'option_value'`指定應該啟用*option_name* （**TRUE**或**on**）或停用（**FALSE**或**off**）。 *option_value*為**Varchar （** 10 **）**，沒有預設值。  
  
 *option_value*可能是「**連接逾時**」和「**查詢超時**」選項的非負整數。 針對 [定**序名稱]** 選項， *option_value*可能是定序名稱或 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 如果 [定**序相容]** 選項設定為 [TRUE]，則定**序名稱**會自動設為 Null。 如果定**序名稱**設定為非 null 值，則自動定**序相容**會設定為 FALSE。  
  
## <a name="permissions"></a>權限  
 需要伺服器的 ALTER ANY LINKED SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會將對應於另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (`SEATTLE3`) 的連結伺服器，設定成定序相容於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機執行個體。  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
## <a name="see-also"></a>另請參閱  
 [分散式查詢預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
