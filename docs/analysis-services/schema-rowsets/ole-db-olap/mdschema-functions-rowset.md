---
title: MDSCHEMA_FUNCTIONS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7e6786f53ddc48c457857f58128c3f16959420d5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="mdschemafunctions-rowset"></a>MDSCHEMA_FUNCTIONS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述可用於與資料庫相連接的用戶端應用程式的函數。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_FUNCTIONS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|Description|  
|-----------------|--------------------|-----------------|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|函數的名稱。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|函數的描述。|  
|**PARAMETER_LIST**|**DBTYPE_WSTR**|以逗號分隔的參數清單，格式化的方式與 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 類似。 例如，參數可能會命名為 String。|  
|**RETURN_TYPE**|**DBTYPE_I4**|**VARTYPE**函式的傳回資料類型。|  
|**來源**|**DBTYPE_I4**|函數的來源：<br /><br /> 1 是 MDX 函數。<br /><br /> 2 是使用者定義函數。|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|使用者定義函數的介面名稱。<br /><br /> 多維度運算式 (MDX) 函數的群組名稱。|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**|使用者定義函數的類型程式庫名稱。 **NULL** MDX 函數。|  
|**DLL_NAME**|**DBTYPE_WSTR**|(選擇性) 實作使用者定義函數之組件的名稱。<br /><br /> 傳回**VT_NULL** MDX 函數。|  
|**HELP_FILE**|**DBTYPE_WSTR**|(選擇性) 檔案的名稱，這個檔案包含使用者定義函數的說明文件集。<br /><br /> 傳回**VT_NULL** MDX 函數。|  
|**HELP_CONTEXT**|**DBTYPE_I4**|(選擇性) 傳回這個函數的說明內容識別碼。|  
|**OBJECT**|**DBTYPE_WSTR**|(選擇性) 屬性所套用至的物件類別的一般名稱。 例如，資料列集對應至 < l >。成員函式會傳回"**層級**"。<br /><br /> 傳回**VT_NULL**使用者定義函式或非屬性的 MDX 函數。|  
|**標題**|**DBTYPE_WSTR**|函數的顯示標題。|  
  
 排序資料列集**原點**， **INTERFACE_NAME**， **FUNCTION_NAME**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_FUNCTIONS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**來源**|**DBTYPE_I4**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
