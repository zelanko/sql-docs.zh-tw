---
title: sp_serveroption (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7bc3948044bbfd37d5ddb5a4dad32f3dc9e09725
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spserveroption-transact-sql"></a>sp_serveroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定遠端伺服器和連結伺服器的伺服器選項。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_serveroption [@server = ] 'server'   
      ,[@optname = ] 'option_name'       
      ,[@optvalue = ] 'option_value' ;  
```  
  
## <a name="arguments"></a>引數  
 [ **@server =** ] **'***server***'**  
 這是要設定選項的伺服器名稱。 *server* 是 **sysname**，沒有預設值。  
  
 [  **@optname =** ] **'***option_name***'**  
 這是要為指定伺服器設定的選項。 *option_name*是**varchar (** 35 **)**，沒有預設值。 *option_name*可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**定序相容**|影響針對連結伺服器的分散式查詢執行。 如果此選項設定為**true**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]假設連結伺服器中的所有字元都都與本機伺服器，關於字元和定序順序 （或排序順序） 相容。 這會使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠將字元資料行的比較傳給提供者。 如果未設定這個選項， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一律會在本機環境中評估字元資料行的比較。<br /><br /> 只有在確定對應於連結伺服器的資料來源與本機伺服器的字元集和排序順序相同時，才應該設定這個選項。|  
|**定序名稱**|指定如果遠端資料來源所使用的定序名稱**使用遠端定序**是**true**和資料來源不是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料來源。 這個名稱必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所支援的定序之一。<br /><br /> 當存取不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但其定序卻符合某項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序的 OLE DB 資料來源時，請使用這個選項。<br /><br /> 連結伺服器必須支援供這部伺服器的所有資料行使用的單一定序。 如果連結伺服器支援單一資料來源內的多重定序，或無法確定連結伺服器的定序是否符合某項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序時，請勿設定這個選項。|  
|**連接逾時**|連接到連結的伺服器逾時出秒數。<br /><br /> 如果**0**，使用**sp_configure**預設值。|  
|**資料存取**|啟用和停用連結伺服器的分散式查詢存取。 僅適用於可以**sys.server**透過新增的項目**sp_addlinkedserver**。|  
|**dist**|散發者。|  
|**延遲結構描述驗證**|判斷是否將檢查遠端資料表的結構描述。<br /><br /> 如果**true**，略過檢查查詢的開始處的遠端資料表的結構描述。|  
|**pub**|簽發者。|  
|**查詢逾時**|針對連結伺服器進行查詢的逾時值。<br /><br /> 如果**0**，使用**sp_configure**預設值。|  
|**rpc**|從給定伺服器啟用 RPC。|  
|**rpc 輸出**|啟用指向給定伺服器的 RPC。|  
|**sub**|訂閱者。|  
|**system**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**使用遠端定序**|決定將使用遠端資料行或本機伺服器的定序。<br /><br /> 如果**true**，遠端資料行的定序會用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料來源，以及在指定的定序**定序名稱**用於非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料來源。<br /><br /> 如果**false**，分散式的查詢一律會使用本機伺服器的預設定序時**定序名稱**遠端資料行的定序也會被忽略。 預設值為 **false**。 ( **False**值是使用中的定序語意相容[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]7.0。)|  
|**遠端程序交易升級**|使用此選項，透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 交易，保護伺服器對伺服器程序的動作。 此選項為 TRUE 時 （或） 呼叫遠端預存程序啟動分散式的交易，並編列利用 MS DTC 交易。 發出遠端預存程序呼叫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是交易發起者，它會控制交易的完成。 當發出連接的後續 COMMIT TRANSACTION 或 ROLLBACK TRANSACTION 陳述式時，負責控制的執行個體會要求 MS DTC 跨越所涉及的各部電腦來管理分散式交易的完成。<br /><br /> 在啟動 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散式交易之後，會向已定義為連結伺服器的其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體發出遠端預存程序呼叫。 所有連結伺服器都會編列在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散式交易中，MS DTC 會確保已針對每部連結伺服器來完成交易。<br /><br /> 如果此選項設定為 FALSE (或 OFF)，在連結伺服器上呼叫遠端預存程序時，本機交易將不會升級為分散式交易。<br /><br /> 如果在進行伺服器對伺服器的程序呼叫之前，此交易已經是分散式交易，則此選項不會有任何影響。 針對連結伺服器執行的程序呼叫將會在相同的分散式交易之下執行。<br /><br /> 如果在進行伺服器對伺服器的程序呼叫之前，連接中沒有任何使用中的交易，則此選項不會有任何影響。 然後此程序會在沒有使用中交易的情況下對連結伺服器執行。<br /><br /> 這個選項的預設值是 TRUE (或 ON)。|  
  
 [  **@optvalue =**] **'***option_value***'**  
 指定是否*option_name*應該啟用 (**TRUE**或**上**) 或停用 (**FALSE**或**關閉**). *option_value*是**varchar (** 10 **)**，沒有預設值。  
  
 *option_value*可能為非負整數**連接逾時**和**查詢逾時**選項。 如**定序名稱**選項， *option_value*可能定序名稱或 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 如果**相容的定序**選項設定為 TRUE，**定序名稱**會自動設為 NULL。 如果**定序名稱**設為非 null 的值，**相容的定序**會自動設為 FALSE。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 ALTER ANY LINKED SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會將對應於另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (`SEATTLE3`) 的連結伺服器，設定成定序相容於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機執行個體。  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
## <a name="see-also"></a>另請參閱  
 [分散式查詢預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpserver & #40;TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
