---
title: "DMSCHEMA_MINING_COLUMNS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DMSCHEMA_MINING_COLUMNS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_COLUMNS rowset
ms.assetid: ae35ccde-4438-46f4-8611-40b2b1a42fce
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 62c211c66076a48261abb39599dfcc47499f6f38
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dmschemaminingcolumns-rowset"></a>DMSCHEMA_MINING_COLUMNS 資料列集
  描述中的所有資料採礦模型的個別資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 這個資料列集會限定為目前的目錄。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_COLUMNS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|Description|  
|-----------------|--------------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|目錄的名稱。 以模型所屬的資料庫名稱來擴展。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|不合格的結構描述名稱。 不支援此資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|採礦模型名稱。 此資料行包含與資料行相關聯的採礦模型名稱，而且它永遠都不會是空的。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|資料行的名稱。|  
|**COLUMN_GUID**|**DBTYPE_GUID**|資料行 GUID。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**COLUMN_PROPID**|**DBTYPE_UI4**|資料行屬性的識別碼。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**|資料行的序數位置。 資料行的編號會從 1 開始。 此資料行包含**NULL**如果沒有資料行沒有穩定的序數值。|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**|布林值，指出資料行是否有預設值。<br /><br /> **TRUE**如果資料行有預設值，否則**FALSE**。|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**|資料行的預設值。<br /><br /> 如果預設值是**NULL**值**COLUMN_HASDEFAULT**包含**TRUE**，且此資料行包含**NULL**。|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**|描述資料行特性的位元遮罩。 **DBCOLUMNFLAGS**列舉型別指定的位元的位元遮罩。 這個資料行永遠都不會是空的。|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|布林值，指出資料行是否可為 Null。<br /><br /> **FALSE**不已知資料行可為 null; 否則如果**TRUE**。|  
|**DATA_TYPE**|**DBTYPE_UI2**|資料行之資料類型的指標。 下列清單示範傳回的指標類型之範例。<br /><br /> 「**資料表**"會傳回**DBTYPE_HCHAPTER**。<br /><br /> 「**文字**"會傳回**DBTYPE_WCHAR**。<br /><br /> 「**長**"會傳回**DBTYPE_I8**。<br /><br /> 「**DOUBLE**"會傳回**DBTYPE_R8**。<br /><br /> 「**日期**"會傳回**DBTYPE_DATE**。|  
|**TYPE_GUID**|**DBTYPE_GUID**|資料行資料類型的 GUID。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**VT_NULL**。|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**|資料欄中值的可能長度上限。 若是字元、二進位或是位元資料行，這是下列其中一個：<br /><br /> 如果有定義長度，則資料行類型分別為字元、位元組或是位元之資料行的最大長度。 例如， **CHAR(5)** SQL 資料表中的資料行的最大長度為 5。<br /><br /> 如果資料行沒有定義的長度，則資料行類型分別為字元、位元組或是位元之資料類型的最大長度。<br /><br /> 如果資料行或是資料類型沒有定義的最大長度，則為零 (0)。<br /><br /> **NULL**對於所有其他類型的資料行|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**|如果資料行類型是字元或是二進位，則為以八位元資料組 (位元組) 為單位之資料行的最大長度。 值為零 (0) 表示資料行沒有最大長度。 此資料行包含**NULL**對於所有其他類型的資料行。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**|如果資料行的資料類型不是數值資料類型的資料行的最大有效位數**VARNUMERIC**。<br /><br /> **NULL**如果資料行的資料類型不是數值，或為**VARNUMERIC**。<br /><br /> 資料行的資料類型的有效位數**DBTYPE_DECIMAL**或**DBTYPE_NUMERIC**取決於資料行定義。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**|如果資料行的類型指標為在小數點右邊的位數**DBTYPE_DECIMAL**， **DBTYPE_NUMERIC**，或**DBTYPE_VARNUMERIC**。 否則，這個資料行會包含**VT_NULL**。|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**|如果資料行資料類型是 DateTime 或是間隔類型，資料行的日期/時間有效位數 （小數秒數部分的位數的數字）否則， **NULL**。|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**|定義字元集的目錄名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**|用於定義字元集的不合格結構描述名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**|字元集名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**|定義定序物件的目錄名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**|用於定義定序的不合格結構描述名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**SYS.DATABASES**|**DBTYPE_WSTR**|定序名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**|定義網域的目錄名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**|用於定義網域的不合格結構描述名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**網域名稱**|**DBTYPE_WSTR**|網域名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|資料行的易記描述此資料行不支援[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**|資料行的統計散發描述。 這個資料行包含下列其中一項：<br /><br /> 「**一般**"<br /><br /> 「**LOG_NORMAL**"<br /><br /> 「**統一**"|  
|**有效**|**DBTYPE_WSTR**|資料行內容的描述。 這個資料行包含下列其中一項：<br /><br /> 「**金鑰**"<br /><br /> 「**離散**"<br /><br /> 「**連續**"<br /><br /> 「**離散化 (**[引數]**)**"<br /><br /> 「**ORDERED**"<br /><br /> 「**KEY TIME**"<br /><br /> 「**CYCLICAL**"<br /><br /> 「**機率**"<br /><br /> 「**變異數**"<br /><br /> 「**STDEV**"<br /><br /> 「**支援**"<br /><br /> 「**PROBABILITY_VARIANCE**"<br /><br /> 「**PROBABILITY_STDEV**"<br /><br /> **「 索引鍵順序**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**|以逗號分隔的旗標清單。 已定義的旗標如下：<br /><br /> 「**MODEL_EXISTENCE_ONLY**"<br /><br /> 「**迴歸輸入變數**"<br /><br /> 演算法特定的模型旗標也可以包含在資料行中。|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**|布林值，指出資料行是否與索引鍵相關。<br /><br /> **TRUE**如果此資料行與索引鍵相關。 如果索引鍵是單一資料行， **RELATED_ATTRIBUTE**欄位可以選擇性地包含其資料行名稱。|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**|與目前的資料行相關或為其特殊屬性的目標資料行名稱。|  
|**IS_INPUT**|**DBTYPE_BOOL**|布林值，指出資料行是否為輸入資料行。<br /><br /> **VARIANT_TRUE**如果這是輸入資料行。|  
|**IS_PREDICTABLE**|**DBTYPE_BOOL**|布林值，指出資料行是否為可預測。<br /><br /> **TRUE**如果可預測的資料行。|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**|名稱**資料表**包含此資料行的資料行。 此資料行包含**NULL**如果資料行不包含在另一個資料行。|  
|**PREDICTION_SCALAR_FUNCTIONS**|**DBTYPE_WSTR**|以逗號分隔的清單，其中列出可在資料行上執行的純量函數。|  
|**PREDICTION_TABLE_FUNCTIONS**|**DBTYPE_WSTR**|以逗號分隔的清單，其中列出可套用至資料行的函數。 函數應該傳回資料表。 此清單具有下列格式：<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> 此格式允許用戶端應用程式針對個別的函數決定簽章 (參數清單)。|  
|**IS_POPULATED**|**DBTYPE_BOOL**|布林值，指出資料行是否已使用一組可能的值來定型。<br /><br /> **TRUE**如果已使用一組可能值的定型資料行。<br /><br /> 包含**FALSE**如果資料行不會擴展。|  
|**PREDICTION_SCORE**|**DBTYPE_R8**|預測資料行之模型的分數。 分數是用以測量模型的精確度。|  
|**SOURCE_COLUMN**|**DBTYPE_WSTR**|目前採礦資料行的來源採礦結構資料行之名稱。|  
  
## <a name="restriction-columns"></a>限制資料行  
 **DMSCHEMA_MINING_COLUMNS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>請參閱＜  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
