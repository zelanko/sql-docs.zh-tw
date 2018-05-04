---
title: DBSCHEMA_PROVIDER_TYPES 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DBSCHEMA_PROVIDER_TYPES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_PROVIDER_TYPES rowset
ms.assetid: 255e01ba-53a9-478d-9b86-45faba76710e
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: caf9cc5b0c178c70889be608d4622b4469f798c1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="dbschemaprovidertypes-rowset"></a>DBSCHEMA_PROVIDER_TYPES 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  識別資料提供者所支援的 (基底) 資料類型。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DBSCHEMA_PROVIDER_TYPES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|Description|  
|-----------------|--------------------|-----------------|  
|**TYPE_NAME**|**DBTYPE_WSTR**|提供者特定的資料類型名稱。|  
|**DATA_TYPE**|**DBTYPE_UI2**|資料類型的指標。|  
|**COLUMN_SIZE**|**DBTYPE_UI4**|非數值資料行或參數的長度，指提供者為此類型定義的最大值或長度。 如果是字元資料，這是最大長度或定義的長度 (以字元為單位)。 如果是 DateTime 資料類型，則此為表示字串的長度 (假設最大值可以容納分數秒元件的有效位數)。<br /><br /> 如果資料類型為數值，此為資料類型最大有效位數的上限。|  
|**LITERAL_PREFIX**|**DBTYPE_WSTR**|在文字命令中做為此類型之常值前置詞的字元。|  
|**LITERAL_SUFFIX**|**DBTYPE_WSTR**|在文字命令中做為此類型之常值後置詞的字元。|  
|**CREATE_PARAMS**|**DBTYPE_WSTR**|建立此資料類型的資料行時，取用者所指定的建立參數。 例如，SQL 資料類型，**小數、**需要精確度及小數位數。 在此情況下，建立參數可能為字串 "precision,scale"。 若要建立文字命令中**十進位**10 位有效位數與小數位數為 2，值的資料行**TYPE_NAME**資料行可能是**DECIMAL()** 和完整的型別規格則為**DECIMAL(10,2)**。<br /><br /> 建立參數會顯示為以逗號分隔的值清單，按提供時的順序列出且不放在括號中。 如果建立參數為長度、最大長度、有效位數、小數位數、種子或增量，請分別使用 "length"、"max length"、"precision"、"scale"、"seed" 和 "increment"。 如果建立參數為其他某值，則提供者會決定要使用什麼文字來描述建立參數。<br /><br /> 如果資料類型需要建立參數，則類型名稱通常會顯示 "()"。 這代表要插入建立參數的位置。 如果類型名稱不包含 "()"，則建立參數會包含在引號中並附加到資料類型名稱。|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|布林值，指出資料類型是否可為 Null。<br /><br /> **VARIANT_TRUE**指出資料類型可為 null。<br /><br /> **VARIANT_FALSE**指出資料類型不可為 null。<br /><br /> **NULL**— 表示，不知道資料型別是否可為 null。|  
|**CASE_SENSITIVE**|**DBTYPE_BOOL**|布林值，指出資料類型是否為字元類型且區分大小寫。<br /><br /> **VARIANT_TRUE**指出資料類型是字元類型且區分大小寫。<br /><br /> **VARIANT_FALSE**表示資料型別不是字元類型，或不區分大小寫。|  
|**可搜尋**|**DBTYPE_UI4**|整數，指出資料類型如何可以用於在搜尋中如果提供者支援**ICommandText**，否則**NULL**。 此資料行可以有下列的值：<br /><br /> **DB_UNSEARCHABLE**指出的資料類型不能在**其中**子句。<br /><br /> **DB_LIKE_ONLY**表示資料型別可以在中使用**其中**子句只能搭配**像**述詞。<br /><br /> **DB_ALL_EXCEPT_LIKE**表示資料型別可以在中使用**其中**子句以外的所有比較運算子搭配**像**。<br /><br /> **DB_SEARCHABLE**表示資料型別可以在中使用**其中**子句搭配任何比較運算子。|  
|**UNSIGNED_ATTRIBUTE**|**DBTYPE_BOOL**|布林值，指出資料類型是否不帶正負號。<br /><br /> **VARIANT_TRUE**指出資料類型是不帶正負號。<br /><br /> **VARIANT_FALSE**指出已簽署的資料類型。<br /><br /> **NULL**指出這是不適用的資料類型。|  
|**FIXED_PREC_SCALE**|**DBTYPE_BOOL**|布林值，指出資料類型是否具有固定的有效位數和小數位數。<br /><br /> **VARIANT_TRUE**表示資料型別具有固定有效位數和小數位數。<br /><br /> **VARIANT_FALSE**表示的資料類型沒有固定有效位數和小數位數。|  
|**AUTO_UNIQUE_VALUE**|**DBTYPE_BOOL**|布林值，指出資料類型是否會自動遞增。<br /><br /> **VARIANT_TRUE**表示此類型的值可以自動遞增。<br /><br /> **VARIANT_FALSE**表示此類型的值不能自動遞增。<br /><br /> 如果此值為**VARIANT_TRUE**、 此類型的資料行一律會自動遞增就取決於提供者是否**DBPROP_COL_AUTOINCREMENT**資料行屬性。 如果**DBPROP_COL_AUTOINCREMENT**屬性是可讀寫，不論此類型的資料行是否自動遞增，取決於設定的**DBPROP_COL_AUTOINCREMENT**屬性。 如果**DBPROP_COL_AUTOINCREMENT**是唯讀屬性，或全部的此類型之資料行不會自動遞增。|  
|**LOCAL_TYPE_NAME**|**DBTYPE_WSTR**|當地語系化的版本**TYPE_NAME**。 **NULL**傳回如果資料提供者不支援當地語系化的名稱。|  
|**MINIMUM_SCALE**|**DBTYPE_I2**|如果類型指標為**DBTYPE_VARNUMERIC**， **DBTYPE_DECIMAL**，或**DBTYPE_NUMERIC**，數字的小數點右邊所允許的最小數目。 否則， **NULL**。|  
|**MAXIMUM_SCALE**|**DBTYPE_I2**|如果類型指標為允許在小數點右邊的位數上限**DBTYPE_VARNUMERIC**， **DBTYPE_DECIMAL**，或**DBTYPE_NUMERIC**，否則為，N**U**LL。|  
|**GUID**|**DBTYPE_GUID**|（供日後使用）**GUID**型別，如果此類型的描述類型程式庫中。 否則， **NULL**。|  
|**型別程式庫**|**DBTYPE_WSTR**|(供日後使用) 如果類型程式庫中有此類型的描述，則為包含該類型描述的類型程式庫； 否則為 NULL。|  
|**VERSION**|**DBTYPE_WSTR**|(供日後使用) 類型定義的版本。 提供者可能會想要對類型定義進行版本控制。 不同的提供者會使用不同的版本控制配置，例如時間戳記或數字 (整數或浮點數)。 **NULL**不受支援。|  
|**IS_LONG**|**DBTYPE_BOOL**|布林值，指出資料類型是否為二進位大型物件 (BLOB) 且具有很長的資料。<br /><br /> **VARIANT_TRUE**指出資料類型為**BLOB**包含很長的資料; 很長資料的定義是特定提供者。<br /><br /> **VARIANT_FALSE**指出資料類型為**BLOB** ，不會包含很長的資料，或者不是**BLOB**。<br /><br /> 這個值會決定的設定**DBCOLUMNFLAGS_ISLONG**所傳回的旗標**GetColumnInfo**中**IColumnsInfo**和**GetParameterInfo**中**ICommandWithParameters**。|  
|**BEST_MATCH**|**DBTYPE_BOOL**|布林值，指出資料類型是否為最符合項目。<br /><br /> **VARIANT_TRUE**表示資料型別是資料存放區中的所有資料型別中的值所指定的 OLE DB 資料類型之間的最佳比對**DATA_TYPE**資料行。<br /><br /> **VARIANT_FALSE**表示資料型別不是最符合項目。<br /><br /> 針對每個資料列集的值**DATA_TYPE**資料行是相同的**BEST_MATCH**資料行設為**VARIANT_TRUE**中只有一個資料列。|  
|**IS_FIXEDLENGTH**|**DBTYPE_BOOL**|布林植，指出資料行的長度是否固定。<br /><br /> **VARIANT_TRUE**表示資料定義語言 (DDL) 所建立此類型的資料行，將會是固定長度。<br /><br /> **VARIANT_FALSE**指出 DDL 建立此類型的資料行所可變長度。<br /><br /> 如果欄位是**NULL**，不知道提供者是否會將此欄位為固定長度或可變長度資料行的對應。|  
  
 排序資料列集**DATA_TYPE**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DBSCHEMA_PROVIDER_TYPES**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|  
|-----------------|--------------------|  
|**DATA_TYPE**|**DBTYPE_UI2**|  
|**BEST_MATCH**|**DBTYPE_BOOL**|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
