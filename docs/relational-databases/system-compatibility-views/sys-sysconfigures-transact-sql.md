---
title: sys.sys設定（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysconfigures
- sysconfigures
- sys.sysconfigures_TSQL
- sysconfigures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconfigures compatibility view
- sysconfigures system table
ms.assetid: 146bf10a-c898-4676-a2a1-673fb1cee7a2
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e0e65f06ccecd01ae9396b2c64962040a446aeb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85663350"
---
# <a name="syssysconfigures-transact-sql"></a>sys.sysconfigures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  針對使用者所設定的每個組態選項，各包含一個資料列。 **sysconfigures**包含最近啟動之前所定義的設定選項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以及自 then 之後所設定的任何動態設定選項。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**value**|**int**|使用者可以修改的變數值。 只有在執行 RECONFIGURE 時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 才會使用這個項目。|  
|**config**|**int**|組態變數號碼。|  
|**加以**|**nvarchar(255)**|組態選項的說明。|  
|**status**|**smallint**|指示選項狀態的點陣圖。 可能的值如下：<br /><br /> 0 = 靜態。 設定在伺服器重新啟動時生效。<br /><br /> 1 = 動態。 變數在執行 RECONFIGURE 陳述式時生效。<br /><br /> 2 = 進階。 只有在已設定**show advanced 選項**時，才會顯示變數。 設定在伺服器重新啟動時生效。<br /><br /> 3 = 動態和進階。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
