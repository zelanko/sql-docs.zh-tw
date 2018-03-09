---
title: "SET FIPS_FLAGGER (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FIPS_FLAGGER
- SET_FIPS_FLAGGER_TSQL
- FIPS_FLAGGER_TSQL
- SET FIPS_FLAGGER
dev_langs:
- TSQL
helpviewer_keywords:
- SET FIPS_FLAGGER statement
- FIPS 127-2 standard
- FIPS_FLAGGER option
ms.assetid: e82f6bee-6cf6-4061-be22-9ad2e8e9d3d6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ece506e0c34f14d827e4562b8c2fcece5de1290d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="set-fipsflagger-transact-sql"></a>SET FIPS_FLAGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定 FIPS 127-2 標準的符合檢查。 這是以 ISO 標準為基礎。 如需 SQL Server FIPS 相容性資訊，請參閱[如何在 FIPS 140-2-相容模式中使用 SQL Server 2016](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode)。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>引數  
 **'** *層級* **'**  
 這是用來檢查所有資料庫作業的 FIPS 127-2 標準之符合層級。 如果資料庫作業相衝突的選擇，ISO 標準層級[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會產生警告。  
  
 *層級*必須是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|ENTRY|符合 ISO 入門層級的標準檢查。|  
|FULL|完全符合 ISO 的標準檢查。|  
|INTERMEDIATE|符合 ISO 中等層級的標準檢查。|  
|OFF|無標準檢查。|  
  
## <a name="remarks"></a>備註  
 設定`SET FIPS_FLAGGER`設定是在剖析階段而不是在執行或執行階段。 在剖析階段設定，表示 SET 陳述式是在批次或預存程序中，如果會生效，不論執行程式碼是否實際到該點。和`SET`陳述式的任何陳述式會在執行之前才會生效。 比方說，即使`SET`陳述式是在`IF...ELSE`陳述式區塊永遠不會在執行期間，達到`SET`陳述式仍會生效，因為`IF...ELSE`會剖析陳述式區塊。  
  
 如果`SET FIPS_FLAGGER`預存程序的值設定`SET FIPS_FLAGGER`預存程序傳回控制權之後還原。 因此，`SET FIPS_FLAGGER`動態 SQL 中所指定的陳述式沒有影響任何動態 SQL 陳述式之後的陳述式。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="see-also"></a>請參閱＜  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
