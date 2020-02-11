---
title: sp_changearticlecolumndatatype （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changearticlecolumndatatype
- sp_changearticlecolumndatatype_TSQL
helpviewer_keywords:
- sp_changearticlecolumndatatype
ms.assetid: 0db80e08-fb77-4d0c-aa41-455b13ffa9b4
author: stevestein
ms.author: sstein
ms.openlocfilehash: f101d9081c7eb898d43c461a3bd64eca0c043b64
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67995521"
---
# <a name="sp_changearticlecolumndatatype-transact-sql"></a>sp_changearticlecolumndatatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更 Oracle 發行集的發行項資料行資料類型對應。 這個預存程序執行於任何資料庫中的散發者端。  
  
> [!NOTE]  
>  依預設，會提供支援的發行者類型之間的資料類型對應。 只有在覆寫這些預設設定時，才使用**sp_changearticlecolumndatatype** 。  
  
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
`[ @publication = ] 'publication'`這是 Oracle 發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @article = ] 'article'`這是發行項的名稱。 *文章*是**sysname**，沒有預設值。  
  
`[ @column = ] 'column'`這是要變更資料類型對應的資料行名稱。 資料*行*是**sysname**，沒有預設值。  
  
`[ @type = ] 'type'`這是目的地[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料行中的資料類型名稱。 *類型*是**sysname**，預設值是 Null。  
  
`[ @length = ] length`這是目的地[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料行中的資料類型長度。 *長度*是**Bigint**，預設值是 Null。  
  
`[ @precision = ] precision`這是目的地[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料行中資料類型的有效位數。 *precision*是**Bigint**，預設值是 Null。  
  
`[ @publisher = ] 'publisher'`指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *publisher*是**sysname**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **Sp_changearticlecolumndatatype**可用來覆寫支援的發行者類型（Oracle 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）之間的預設資料類型對應。 若要查看這些預設資料類型對應，請執行[sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)。  
  
 只有 Oracle 發行者才支援**sp_changearticlecolumndatatype** 。 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集執行這個預存程序會發生錯誤。  
  
 必須針對必須變更的每個發行項資料行對應執行**sp_changearticlecolumndatatype** 。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_changearticlecolumndatatype**。  
  
## <a name="see-also"></a>另請參閱  
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
