---
title: "p (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_changearticlecolumndatatype
- sp_changearticlecolumndatatype_TSQL
helpviewer_keywords: sp_changearticlecolumndatatype
ms.assetid: 0db80e08-fb77-4d0c-aa41-455b13ffa9b4
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1defb009948d01147e4b8f9e333cdd108c8bbba9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spchangearticlecolumndatatype-transact-sql"></a>sp_changearticlecolumndatatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更 Oracle 發行集的發行項資料行資料類型對應。 這個預存程序執行於任何資料庫中的散發者端。  
  
> [!NOTE]  
>  依預設，會提供支援的發行者類型之間的資料類型對應。 使用**sp_changearticlecolumndatatype**才覆寫這些預設設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changearticlecolumndatatype [ @publication= ] 'publication'  
    [ @article = ] 'article'   
    [ @column = ] 'column'  
    [ , [ @type = ] 'type' ]  
    [ , [ @length = ] length ]  
    [ , [ @precision = ] precision ]  
    [ , [ @scale = ] scale ]  
    [ , [ @publisher = ] 'publisher'  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=** ] **'***發行集***'**  
 這是 Oracle 發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@article =** ] **'***文章***'**  
 這是發行項的名稱。 *發行項*是**sysname**，沒有預設值。  
  
 [  **@column** =] **'***資料行***'**  
 這是要變更資料類型對應的資料行名稱。 *資料行*是**sysname**，沒有預設值。  
  
 [  **@type**  =] **'***類型***'**  
 名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目的地資料行中的資料類型。 *型別*是**sysname**，預設值是 NULL。  
  
 [  **@length**  =]*長度*  
 是目的地資料行中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的長度。 *長度*是**bigint**，預設值是 NULL。  
  
 [  **@precision** =]*有效位數*  
 是目的地資料行中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的有效位數。 *有效位數*是**bigint**，預設值是 NULL。  
  
 [  **@publisher** =] **'***發行者***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **Sp_changearticlecolumndatatype**用來覆寫支援的發行者類型之間的預設資料類型對應 (Oracle 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。 若要檢視這些預設資料類型對應，請執行[sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)。  
  
 **sp_changearticlecolumndatatype**只支援 Oracle 發行者。 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集執行這個預存程序會發生錯誤。  
  
 **sp_changearticlecolumndatatype**必須針對每個發行項的資料行對應必須變更執行。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_changearticlecolumndatatype**。  
  
## <a name="see-also"></a>請參閱＜  
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
