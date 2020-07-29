---
title: Index 元素 (DTA)
description: 在 DTA 公用程式中，Index 元素包含要針對使用者所指定組態建立或卸除的索引資訊。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Index element (DTA)
ms.assetid: 447d3964-b387-40f6-9189-71386774c29e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 4151e138347ad09f8e32dbd0f96e8e7a9a5ff83e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732091"
---
# <a name="index-element-dta"></a>Index 元素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

包含您要建立或卸除的使用者指定組態索引的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Recommendation>  
  <Create>  
    <Index [Clustered | Unique | Online | IndexSizeInMB | NumberOfRows             | QUOTED_IDENTIFIER | ARITHABORT | CONCAT_NULL_YIELDS_NULL             | ANSI_NULLS | ANSI_PADDING | ANSI_WARNINGS  
            | NUMERIC_ROUNDABORT]  
     ...code removed here...  
    </Index>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|索引屬性|資料類型|描述|  
|---------------------|---------------|-----------------|  
|**叢集**|**boolean**|選擇性。 指定叢集索引。 設為 "true" 或 "false"，例如：<br /><br /> `<Index Clustered="true">`<br /><br /> 依預設，這個屬性設為 "false"。|  
|**唯一**|**boolean**|選擇性。 指定唯一索引。 設為 "true" 或 "false"，例如：<br /><br /> `<Index Unique="true">`<br /><br /> 依預設，這個屬性設為 "false"。|  
|**線上存取**|**boolean**|選擇性。 指定伺服器在線上時，能夠執行作業的索引，需要暫存磁碟空間。 設為 "true" 或 "false"，例如：<br /><br /> `<Index Online="true">`<br /><br /> 依預設，這個屬性設為 "false"。<br /><br /> 如需詳細資訊，請參閱 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)。|  
|**IndexSizeInMB**|**double**|選擇性。 指定索引的大小上限 (MB)，例如：<br /><br /> `<Index IndexSizeInMB="873.75">`<br /><br /> 沒有預設值。|  
|**NumberOfRows**|**integer**|選擇性。 模擬不同的索引大小，它能夠有效模擬不同的資料表大小，例如：<br /><br /> `<Index NumberOfRows="3000">`<br /><br /> 沒有預設值。|  
|**QUOTED_IDENTIFIER**|**boolean**|選擇性。 在分隔識別碼與文字字串的引號方面，使 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 遵循該 ISO 規則。 如果索引是在計算資料行或檢視上，就必須開啟這個屬性。 例如，下列語法會將這個屬性設為開啟：<br /><br /> `<Index QUOTED_IDENTIFIER [...]>`<br /><br /> 依預設，會關閉這個屬性。<br /><br /> 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。|  
|**ARITHABORT**|**boolean**|選擇性。 在查詢執行期間，當發生溢位或除以零的錯誤時，會使查詢終止。 如果索引是在計算資料行或檢視上，就必須開啟這個屬性。 例如，下列語法會將這個屬性設為開啟：<br /><br /> `<Index ARITHABORT [...]>`<br /><br /> 依預設，會關閉這個屬性。<br /><br /> 如需詳細資訊，請參閱 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)。|  
|**CONCAT_NULL_YIELDS_**<br /><br /> **NULL**|**boolean**|選擇性。 控制是否將串連結果當作 Null 或空字串值來處理。 如果索引是在計算資料行或檢視上，就必須開啟這個屬性。 例如，下列語法會將這個屬性設為開啟：<br /><br /> `<Index CONCAT_NULL_YIELDS_NULL [...]>`<br /><br /> 依預設，會關閉這個屬性。<br /><br /> 如需詳細資訊，請參閱 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)。|  
|**ANSI_NULLS**|**boolean**|選擇性。 指定搭配 null 值一起使用時，等於 (=) 和不等於 (<>) 比較運算子的 ISO 相容行為。 如果索引是在計算資料行或檢視上，就必須開啟這個屬性。 例如，下列語法會將這個屬性設為開啟：<br /><br /> `<Index ANSI_NULLS [...]>`<br /><br /> 依預設，會關閉這個屬性。<br /><br /> 如需詳細資訊，請參閱 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)。|  
|**ANSI_PADDING**|**boolean**|選擇性。 控制資料行儲存比定義大小短之值的方式。 如果索引是在計算資料行或檢視上，就必須開啟這個屬性。 例如，下列語法會將這個屬性設為開啟：<br /><br /> `<Index ANSI_PADDING [...]>`<br /><br /> 依預設，會關閉這個屬性。<br /><br /> 如需詳細資訊，請參閱 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)。|  
|**ANSI_WARNINGS**|**boolean**|選擇性。 指定數個錯誤狀況的 ISO 標準行為。 如果索引是在計算資料行或檢視上，就必須開啟這個屬性。 例如，下列語法會將這個屬性設為開啟：<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> 依預設，會關閉這個屬性。<br /><br /> 如需詳細資訊，請參閱 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)。|  
|**NUMERIC_ROUNDABORT**|**boolean**|選擇性。 指定在運算式中因捨入而造成失去精確度時，所產生的錯誤報告層級。 如果索引是在計算資料行或檢視的索引，就必須關閉這個屬性。<br /><br /> 下列語法會將這個屬性設為開啟：<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> 依預設，會關閉這個屬性。<br /><br /> 如需詳細資訊，請參閱 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)。|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|如果未利用 **Create** 或 **Drop** 元素來指定任何其他實體設計結構，每個 **Statistics** 或 **Heap** 元素需要使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Create 元素 &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> **Drop** 元素。 如需詳細資訊，請參閱＜Database Engine Tuning Advisor XML 結構描述＞。|  
|**子元素**|[索引的 Name 元素 &#40;DTA&#41;](../../tools/dta/name-element-for-index-dta.md)<br /><br /> [索引的 Column 元素 &#40;DTA&#41;](../../tools/dta/column-element-for-index-dta.md)<br /><br /> **PartitionScheme** 元素。 如需詳細資訊，請參閱＜Database Engine Tuning Advisor XML 結構描述＞。<br /><br /> **PartitionColumn** 元素。 如需詳細資訊，請參閱＜Database Engine Tuning Advisor XML 結構描述＞。<br /><br /> [索引的 Filegroup 元素 &#40;DTA&#41;](../../tools/dta/filegroup-element-for-index-dta.md)<br /><br /> **NumberOfReferences** 元素。 如需詳細資訊，請參閱＜Database Engine Tuning Advisor XML 結構描述＞。<br /><br /> **PercentUsage** 元素。 如需詳細資訊，請參閱＜Database Engine Tuning Advisor XML 結構描述＞。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
