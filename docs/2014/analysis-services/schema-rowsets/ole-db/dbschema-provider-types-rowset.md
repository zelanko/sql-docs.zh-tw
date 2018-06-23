---
title: DBSCHEMA_PROVIDER_TYPES 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DBSCHEMA_PROVIDER_TYPES
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_PROVIDER_TYPES rowset
ms.assetid: 255e01ba-53a9-478d-9b86-45faba76710e
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1c26c713f7032038b3cb969ff7681dc23c7deea2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136084"
---
# <a name="dbschemaprovidertypes-rowset"></a>DBSCHEMA_PROVIDER_TYPES 資料列集
  識別資料提供者所支援的 (基底) 資料類型。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DBSCHEMA_PROVIDER_TYPES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`TYPE_NAME`|`DBTYPE_WSTR`||提供者特定的資料類型名稱。|  
|`DATA_TYPE`|`DBTYPE_UI2`||資料類型的指標。|  
|`COLUMN_SIZE`|`DBTYPE_UI4`||非數值資料行或參數的長度，指提供者為此類型定義的最大值或長度。 如果是字元資料，這是最大長度或定義的長度 (以字元為單位)。 如果是 DateTime 資料類型，則此為表示字串的長度 (假設最大值可以容納分數秒元件的有效位數)。<br /><br /> 如果資料類型為數值，此為資料類型最大有效位數的上限。|  
|`LITERAL_PREFIX`|`DBTYPE_WSTR`||在文字命令中做為此類型之常值前置詞的字元。|  
|`LITERAL_SUFFIX`|`DBTYPE_WSTR`||在文字命令中做為此類型之常值後置詞的字元。|  
|`CREATE_PARAMS`|`DBTYPE_WSTR`||建立此資料類型的資料行時，取用者所指定的建立參數。 例如，SQL 資料類型 `DECIMAL,` 需要有效位數及小數位數。 在此情況下，建立參數可能為字串 "precision,scale"。 在有效位數為 10，小數位數為 2 且用於建立 `DECIMAL` 資料行的文字命令中，`TYPE_NAME` 資料行的值可能為 `DECIMAL()`，完整的類型規格則為 `DECIMAL(10,2)`。<br /><br /> 建立參數會顯示為以逗號分隔的值清單，按提供時的順序列出且不放在括號中。 如果建立參數為長度、最大長度、有效位數、小數位數、種子或增量，請分別使用 "length"、"max length"、"precision"、"scale"、"seed" 和 "increment"。 如果建立參數為其他某值，則提供者會決定要使用什麼文字來描述建立參數。<br /><br /> 如果資料類型需要建立參數，則類型名稱通常會顯示 "()"。 這代表要插入建立參數的位置。 如果類型名稱不包含 "()"，則建立參數會包含在引號中並附加到資料類型名稱。|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||布林值，指出資料類型是否可為 Null。<br /><br /> `VARIANT_TRUE` 指出資料類型可為 Null。<br /><br /> `VARIANT_FALSE` 指出資料類型不可為 null。<br /><br /> `NULL`— 指出不知道資料類型是否可為 Null。|  
|`CASE_SENSITIVE`|`DBTYPE_BOOL`||布林值，指出資料類型是否為字元類型且區分大小寫。<br /><br /> `VARIANT_TRUE` 指出資料類型為字元類型且區分大小寫。<br /><br /> `VARIANT_FALSE` 指出資料類型並非字元類型且不區分大小寫。|  
|`SEARCHABLE`|`DBTYPE_UI4`||整數，指出如果提供者支援 `ICommandText`，如何在搜尋中使用資料類型；否則為 `NULL`。<br /><br /> 此資料行可以有下列的值：<br /><br /> -   `DB_UNSEARCHABLE` 表示資料型別無法在使用`WHERE`子句。<br />-   `DB_LIKE_ONLY` 表示資料型別可以在中使用`WHERE`子句只能搭配`LIKE`述詞。<br />-   `DB_ALL_EXCEPT_LIKE` 表示資料型別可以在中使用`WHERE`子句以外的所有比較運算子搭配`LIKE`。<br />-   `DB_SEARCHABLE` 表示資料型別可以在中使用`WHERE`子句搭配任何比較運算子。|  
|`UNSIGNED_ATTRIBUTE`|`DBTYPE_BOOL`||布林值，指出資料類型是否不帶正負號。<br /><br /> `VARIANT_TRUE` 指出資料類型不帶正負號。<br /><br /> `VARIANT_FALSE` 指出資料類型帶正負號。<br /><br /> `NULL` 指出這不適用於資料類型。|  
|`FIXED_PREC_SCALE`|`DBTYPE_BOOL`||布林值，指出資料類型是否具有固定的有效位數和小數位數。<br /><br /> `VARIANT_TRUE` 指出資料類型具有固定的有效位數和小數位數。<br /><br /> `VARIANT_FALSE` 指出資料類型沒有固定的有效位數和小數位數。|  
|`AUTO_UNIQUE_VALUE`|`DBTYPE_BOOL`||布林值，指出資料類型是否會自動遞增。<br /><br /> `VARIANT_TRUE` 指出這個類型的值可以自動遞增。<br /><br /> `VARIANT_FALSE` 指出這個類型的值不能自動遞增。<br /><br /> 如果這個值為 `VARIANT_TRUE`，則這個類型的資料行是否一定會自動遞增，取決於提供者的 `DBPROP_COL_AUTOINCREMENT` 資料行屬性。 如果 `DBPROP_COL_AUTOINCREMENT` 是可讀取/寫入的屬性，這個類型的資料行是否會自動遞增就取決於 `DBPROP_COL_AUTOINCREMENT` 屬性的設定。 如果 `DBPROP_COL_AUTOINCREMENT` 是唯讀屬性，則這個類別的資料行全部都會自動遞增或全部不會自動遞增。|  
|`LOCAL_TYPE_NAME`|`DBTYPE_WSTR`||`TYPE_NAME` 的當地語系化版本。 如果資料提供者不支援當地語系化名稱，便傳回 `NULL`。|  
|`MINIMUM_SCALE`|`DBTYPE_I2`||如果類型指標為 `DBTYPE_VARNUMERIC`、`DBTYPE_DECIMAL` 或 `DBTYPE_NUMERIC`，則此為小數點右邊所允許的最小位數； 否則， `NULL`。|  
|`MAXIMUM_SCALE`|`DBTYPE_I2`||如果類型指標為 `DBTYPE_VARNUMERIC`、`DBTYPE_DECIMAL` 或 `DBTYPE_NUMERIC`，則此為小數點右邊所允許的最大位數；否則為 N`U`LL。|  
|`GUID`|`DBTYPE_GUID`||(供日後使用) 如果類型程式庫中有此類型的描述，則為該類型的 `GUID`； 否則， `NULL`。|  
|`TYPELIB`|`DBTYPE_WSTR`||(供日後使用) 如果類型程式庫中有此類型的描述，則為包含該類型描述的類型程式庫； 否則為 NULL。|  
|`VERSION`|`DBTYPE_WSTR`||(供日後使用) 類型定義的版本。 提供者可能會想要對類型定義進行版本控制。 不同的提供者會使用不同的版本控制配置，例如時間戳記或數字 (整數或浮點數)。 如果未支援則為 `NULL`。|  
|`IS_LONG`|`DBTYPE_BOOL`||布林值，指出資料類型是否為二進位大型物件 (BLOB) 且具有很長的資料。<br /><br /> `VARIANT_TRUE` 表示資料類型為包含很長資料的 `BLOB`；很長資料的定義依特定的提供者而定。<br /><br /> `VARIANT_FALSE` 指出資料類型為不包含很長資料的 `BLOB` 或並非 `BLOB`。<br /><br /> 此值決定 `DBCOLUMNFLAGS_ISLONG` 旗標的設定，這個旗標會由 `GetColumnInfo` 中的 `IColumnsInfo` 傳回，也會由 `GetParameterInfo` 中的 `ICommandWithParameters` 傳回。|  
|`BEST_MATCH`|`DBTYPE_BOOL`||布林值，指出資料類型是否為最符合項目。<br /><br /> `VARIANT_TRUE` 指出資料類型為資料存放區中的所有資料類型與 `DATA_TYPE` 資料行中的值所代表的 OLE DB 資料類型之間的最符合項目。<br /><br /> `VARIANT_FALSE` 指出資料類型並非最符合項目。<br /><br /> 對於 `DATA_TYPE` 資料行的值都相同的每個資料列集，`BEST_MATCH` 資料行僅會在一個資料列中設定為 `VARIANT_TRUE`。|  
|`IS_FIXEDLENGTH`|`DBTYPE_BOOL`||布林植，指出資料行的長度是否固定。<br /><br /> `VARIANT_TRUE` 指出資料定義語言 (DDL) 所建立的此類型資料行為固定長度。<br /><br /> `VARIANT_FALSE` 指出 DDL 所建立的此類型資料行為可變長度。<br /><br /> 如果欄位為 `NULL`，表示仍不知道提供者會將此欄位對應至固定長度或是可變長度資料行。|  
  
 資料列集會按 `DATA_TYPE` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DBSCHEMA_PROVIDER_TYPES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`DATA_TYPE`|`DBTYPE_UI2`||  
|`BEST_MATCH`|`DBTYPE_BOOL`||  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 結構描述資料列集](ole-db-schema-rowsets.md)  
  
  