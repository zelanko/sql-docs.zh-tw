---
title: sp_publisherproperty & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_publisherproperty
- sp_publisherproperty_TSQL
helpviewer_keywords:
- sp_publisherproperty
ms.assetid: 0ed1ebc1-a1bd-4aed-9f46-615c5cf07827
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 37b94b68702394b73ae810b246c0701e876802de
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023251"
---
# <a name="sppublisherproperty-transact-sql"></a>sp_publisherproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示或變更 「 發行者 」 屬性為非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 這個預存程序執行於散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>引數  
 [**@publisher** =] **'***發行者***'**  
 這是異質性發行者的名稱。 *發行者*已**sysname**，沒有預設值。  
  
 [**@propertyname** =] **'***propertyname***'**  
 這是要設定之屬性的名稱。 *propertyname*已**sysname**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**propertyname**|如果發行者端的交易分組成在交易上一致的各個組 (稱為 Xactsets)，以便進行後續處理。 值為**啟用**表示，可以建立 Xactsets，這是預設值。 值為**停用**所建立的任何新 xactsets 的方式處理現有的 Xactsets 的方式。|  
|**propertyname**|如果啟用建立 Xactsets 的 Xactsets 作業， 值為**啟用**表示定期執行 Xactset 作業： 在 「 發行者 」 端建立 Xactsets。 值為**停用**表示，才建立 Xactsets 記錄讀取器代理程式時，它會輪詢 「 發行者 」 進行變更。|  
|**xactsetjobinterval**|Xactset 作業的執行間隔 (以分鐘為單位)。|  
  
 當*propertyname*省略則會傳回所有可設定的屬性。  
  
 [**@propertyvalue** =] **'***propertyvalue***'**  
 這是屬性設定的新值。 *propertyvalue*已**sysname**，預設值是 NULL。 當*propertyvalue*省略，則目前的設定會傳回屬性。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|傳回下列可設定的發行集屬性：<br /><br /> **propertyname**<br /><br /> **propertyname**<br /><br /> **xactsetjobinterval**|  
|**propertyvalue**|**sysname**|是中的屬性的目前設定**propertyname**資料行。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_publisherproperty**用於異動複寫的非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 當只有*發行者*指定，結果集會包含可以設定的所有屬性的目前設定。  
  
 當*propertyname*指定，則只能使用具名的屬性會出現在結果集。  
  
 當指定所有參數時，屬性會改變，不會傳回結果集。  
  
 變更時**xactsetjobinterval**執行中工作的屬性，您必須重新啟動的作業，新的間隔，才會生效。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**散發者端的固定的伺服器角色可以執行**sp_publisherproperty**。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者的交易集作業 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
