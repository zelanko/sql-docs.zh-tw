---
title: DMSCHEMA_MINING_STRUCTURE_COLUMNS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 722adc702e40df68c4a137fb15120c81bcdef90d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingstructurecolumns-rowset"></a>DMSCHEMA_MINING_STRUCTURE_COLUMNS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述正在執行的伺服器上部署的所有採礦結構的個別資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_STRUCTURE_COLUMNS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||目錄的名稱。|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||不合格的結構描述名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支援結構描述，因此這個資料行一律是**NULL**。|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**||結構名稱。 此資料行不能包含**NULL**。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**||資料行的名稱。 只有在共用相同模式的資料行之間可保證唯一性。 例如，如果它們在相同結構中屬於兩個不同的巢狀資料表，則這兩個巢狀資料行可能會有相同的名稱。|  
|**COLUMN_GUID**|**DBTYPE_GUID**||資料行 GUID。 不使用 Guid 來識別資料行的提供者應傳回**NULL**這個資料行中。|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||資料行屬性的識別碼。 請勿將屬性 Id 關聯的資料行的提供者應傳回**NULL**這個資料行中。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 傳回**NULL**此資料行。|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||資料行的序數。 資料行的編號會從 1 開始。 **NULL**如果沒有資料行沒有穩定的序數值。|  
|**COLUMN_HASDEFAULT**|**DBTYPE_BOOL**||布林值，指出資料行是否有預設值。<br /><br /> **TRUE**資料行有預設值。<br /><br /> **FALSE**資料行沒有預設值，或者它是未知的資料行是否具有預設值。|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||資料行的預設值。 提供者可能會公開**DBCOLUMN_DEFAULTVALUE**但不是**DBCOLUMN_HASDEFAULT** （適用於 ISO 資料表） 中所傳回的資料列集**icolumnsrowset:: Getcolumnsrowset**。<br /><br /> 如果預設值是**NULL**， **COLUMN_HASDEFAULT**是**TRUE**和**COLUMN_DEFAULT**資料行是**NULL**值。|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||描述資料行特性的位元遮罩。 **DBCOLUMNFLAGS**列舉型別指定的位元的位元遮罩。 此資料行不能包含**NULL**值。 有效值包括：<br /><br /> **DBCOLUMNFLAGS_ISNULLABLE** (**0x20**)<br /><br /> **DBCOLUMNFLAGS_MAYBENULL** (**0x40**)<br /><br /> **DBCOLUMNFLAGS_ISLONG** (**0x80**)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||布林值，指出資料行是否有預設值。<br /><br /> **TRUE**如果資料行可以包含**NULL**;**FALSE**，否則為。|  
|**DATA_TYPE**|**DBTYPE_UI2**||資料行之資料類型的指標。 例如：<br /><br /> 「**資料表**"= **DBTYPE_HCHAPTER**<br /><br /> 「**文字**"= **DBTYPE_WCHAR**<br /><br /> 「**長**"= **DBTYPE_I8**<br /><br /> 「**DOUBLE**"= **DBTYPE_R8**<br /><br /> 「**日期**"= **DBTYPE_DATE**|  
|**TYPE_GUID**|**DBTYPE_GUID**||資料行資料類型的 GUID。 不使用 Guid 來識別資料類型的提供者應傳回**NULL**這個資料行中。|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||資料欄中值的可能長度上限。 若是字元、二進位或是位元資料行，這是下列其中一個：<br /><br /> 如果有定義長度，則分別為字元、位元組或是位元之資料行的最大長度。 例如，SQL 資料表中的 `CHAR(5)` 資料行其最大的長度為 5。<br /><br /> 如果資料行沒有定義的長度，則分別為字元、位元組或是位元之資料類型的最大長度。<br /><br /> 如果資料行或是資料類型沒有定義的最大長度，則為零 (0)。<br /><br /> **NULL**對於所有其他類型的資料行。|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||如果資料行類型是字元或是二進位，則為以八位元資料組 (位元組) 為單位之資料行的最大長度。 值為零 (0) 表示資料行沒有最大長度。 **NULL**對於所有其他類型的資料行。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||如果資料行的資料類型不是數值資料類型的資料行的最大有效位數**VARNUMERIC**;**NULL**如果資料行的資料類型不是數值，或為**VARNUMERIC**。<br /><br /> 資料行的資料類型的有效位數**DBTYPE_DECIMAL**或**DBTYPE_NUM**ERIC 取決於資料行的定義。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||如果資料行的類型指標為在小數點右邊的位數**DBTYPE_DECIMAL**， **DBTYPE_NUMERIC**，或**DBTYPE_VARNUMERIC**。 否則，這是**NULL**。|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||如果資料行是日期時間或是間隔類型，則為資料行的 DateTime 有效位數 (毫秒部分的位數)。 如果資料行的資料類型不是 datetime，這是**NULL**。|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||定義字元集的目錄名稱。 **NULL**如果提供者不支援目錄或是不同的字元集。|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||定義字元集之不合格的結構描述名稱。 **NULL**如果提供者不支援結構描述或是不同的字元集。|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||字元集名稱。 **NULL**如果提供者不支援不同的字元集。|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||定義定序物件的目錄名稱。 **NULL**如果提供者不支援目錄或是不同的定序。|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||定義定序之不合格的結構描述名稱。 **NULL**如果提供者不支援結構描述或是不同的定序。|  
|**SYS.DATABASES**|**DBTYPE_WSTR**||定序名稱。 **NULL**如果提供者不支援不同定序。|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||定義網域的目錄名稱。 **NULL**如果提供者不支援目錄或是網域。|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||用於定義網域的不合格結構描述名稱。 **NULL**如果提供者不支援結構描述或是網域。|  
|**網域名稱**|**DBTYPE_WSTR**||網域名稱。 **NULL**如果提供者不支援的網域。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||人們可讀取的資料行描述。 **NULL**是否有任何資料行相關聯的描述。|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**||採礦結構資料行的散發：<br /><br /> 「**一般**"<br /><br /> 「**LOG_NORM**AL"<br /><br /> 「**統一**"|  
|**有效**|**DBTYPE_WSTR**||採礦結構資料行的內容類型：<br /><br /> 「**金鑰**"<br /><br /> 「**離散**"<br /><br /> 「**連續**"<br /><br /> 「**離散化 (**[args]**)**"<br /><br /> 「**ORDERED**"<br /><br /> 「**SEQUENCE_TIME**"<br /><br /> 「**CYCLICAL**"<br /><br /> 「**機率**"<br /><br /> 「**變異數**"<br /><br /> 「**STDEV**"<br /><br /> 「**支援**"<br /><br /> 「**PROBABILITY_VARIANCE**"<br /><br /> 「**PROBABILITY_STDEV**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**||以逗號分隔的模型旗標清單。 唯一支援的旗標的結構資料行 」**NOT NULL**"。|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**||指出此資料行是否與索引鍵相關的布林值。<br /><br /> **VARIANT_TRUE**如果此資料行與索引鍵**VARIANT_FALSE**否則。 如果索引鍵是單一資料行， **RELATED_ATTRIBUTE**欄位 （選擇性） 可能會包含其資料行名稱。|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**||目標資料行名稱，與目前的資料行相關，或是目前的資料行為其特殊屬性。|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**||名稱**資料表**包含此資料行的資料行。 **NULL**如果沒有資料表包含資料行。|  
|**IS_POPULATED**|**DBTYPE_BOOL**||布林值，指出此資料行是否已取得一組可能的值。<br /><br /> **TRUE**如果資料行已取得一組可能的值**FALSE**，否則為。|  
  
## <a name="restriction-columns"></a>限制資料行  
 **DMSCHEMA_MINING_STRUCTURE_COLUMNS**上表中的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|選擇性。|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|選擇性。|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
