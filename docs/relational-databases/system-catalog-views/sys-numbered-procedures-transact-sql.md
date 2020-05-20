---
title: sys.databases numbered_procedures （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.numbered_procedures_TSQL
- numbered_procedures
- sys.numbered_procedures
- numbered_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedures catalog view
ms.assetid: 5b6d6498-bac6-4266-94b9-d16ef5089cf0
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ec4ee023960c573ac48ff66886181c2f88b374bb
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82825049"
---
# <a name="sysnumbered_procedures-transact-sql"></a>sys.numbered_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  針對建立為編號程序的每個 SQL Server 預存程序，各包含一個資料列。 這並不會顯示基底 (數字 = 1) 預存程序的一個資料列。 基底預存程式的專案可以在如**sys.databases**和**sys.databases**等視圖中找到。  
  
> [!IMPORTANT]  
>  編號程序已被取代。 不再使用編號程序。 當編譯使用這份目錄檢視的查詢時，會引發 DEPRECATION_ANNOUNCEMENT 事件。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|預存程序的物件識別碼。|  
|**procedure_number**|**smallint**|這個程序在物件內的編號，大於或等於 2。|  
|**definition**|**nvarchar(max)**|定義這個程序的 SQL Server 文字。<br /><br /> NULL = 已加密。|  
  
> [!NOTE]  
>  編號程序並不支援 XML 和 CLR 參數。  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
