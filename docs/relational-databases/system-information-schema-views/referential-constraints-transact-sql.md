---
title: REFERENTIAL_CONSTRAINTS （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- REFERENTIAL_CONSTRAINTS
- REFERENTIAL_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS view
- REFERENTIAL_CONSTRAINTS view
ms.assetid: 5d358f18-0a85-4b55-af4b-98d5f4cd1020
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c4b4d63a7ff49b580205415df4c2b428a07874e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103259"
---
# <a name="referential_constraints-transact-sql"></a>REFERENTIAL_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫中的每個 FOREIGN KEY 條件約束，各傳回一個資料列。 這個資訊結構描述檢視會傳回目前使用者有權限的物件之相關資訊。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**Nvarchar （** 128 **）**|條件約束限定詞。|  
|**CONSTRAINT_SCHEMA**|**Nvarchar （** 128 **）**|包含條件約束之結構描述的名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**CONSTRAINT_NAME**|**sysname**|條件約束名稱。|  
|**UNIQUE_CONSTRAINT_CATALOG**|**Nvarchar （** 128 **）**|UNIQUE 條件約束限定詞。|  
|**UNIQUE_CONSTRAINT_SCHEMA**|**Nvarchar （** 128 **）**|包含 UNIQUE 條件約束的結構描述名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**UNIQUE_CONSTRAINT_NAME**|**sysname**|UNIQUE 條件約束。|  
|**MATCH_OPTION**|**Varchar （** 7 **）**|參考條件約束相符狀況。 一律傳回 SIMPLE。 這表示未定義相符項目。 當符合下列條件之一時，狀況就視為相符：<br /><br /> 外部索引鍵資料行至少有一個值是 NULL。<br /><br /> 外部索引鍵資料行中的所有值都不是 NULL，且主索引鍵資料表中有一個含相同索引鍵的資料列。|  
|**UPDATE_RULE**|**Varchar （** 11 **）**|當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式違反這個條件約束所定義的參考完整性時，所採取的動作。 傳回下列項目之一： <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> 如果這個條件約束的 ON UPDATE 指定了 NO ACTION，就不會將條件約束所參考的主索引鍵之更新傳播到外部索引鍵。 如果這類的主索引鍵更新會因為至少有一個外部索引鍵包含相同的值，而造成參考完整性違規，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會變更父系和參考資料表。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也會引發錯誤。<br /><br /> 如果這個條件約束的 ON UPDATE 指定了 CASCADE，就會將主索引鍵值的變更傳播到外部索引鍵值。|  
|**DELETE_RULE**|**Varchar （** 11 **）**|當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式違反這個條件約束所定義的參考完整性時，所採取的動作。 傳回下列項目之一： <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> 如果這個條件約束的 ON DELETE 指定了 NO ACTION，就不會將條件約束所參考的主索引鍵之刪除傳播到外部索引鍵。 如果這類的主索引鍵刪除會因為至少有一個外部索引鍵包含相同的值，而造成參考完整性違規，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會變更父系和參考資料表。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也會引發錯誤。<br /><br /> 如果這個條件約束的 ON DELETE 指定了 CASCADE，就會將主索引鍵值的變更傳播到外部索引鍵值。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊架構視圖 &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [foreign_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
