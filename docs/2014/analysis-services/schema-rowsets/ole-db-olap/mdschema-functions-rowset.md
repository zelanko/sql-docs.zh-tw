---
title: MDSCHEMA_FUNCTIONS 資料列集 |Microsoft 文件
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
- MDSCHEMA_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_FUNCTIONS rowset
ms.assetid: 5253fa8c-b1ce-4504-aff6-a246b5e675c7
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8e3086730ad66a0f21d9cc458d34d96a6d0eacc3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132528"
---
# <a name="mdschemafunctions-rowset"></a>MDSCHEMA_FUNCTIONS 資料列集
  描述可用於與資料庫相連接的用戶端應用程式的函數。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_FUNCTIONS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**||函數的名稱。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||函數的描述。|  
|**PARAMETER_LIST**|**DBTYPE_WSTR**||以逗號分隔的參數清單，格式化的方式與 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 類似。 例如，參數可能會命名為 String。|  
|**RETURN_TYPE**|**DBTYPE_I4**||**VARTYPE**函式的傳回資料類型。|  
|**來源**|**DBTYPE_I4**||函數的來源：<br /><br /> -1 是 MDX 函數。<br />-2。 使用者定義函數。|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**||使用者定義函數的介面名稱。<br /><br /> 多維度運算式 (MDX) 函數的群組名稱。|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**||使用者定義函數的類型程式庫名稱。 **NULL** MDX 函數。|  
|**DLL_NAME**|**DBTYPE_WSTR**||(選擇性) 實作使用者定義函數之組件的名稱。<br /><br /> 傳回**VT_NULL** MDX 函數。|  
|**HELP_FILE**|**DBTYPE_WSTR**||(選擇性) 檔案的名稱，這個檔案包含使用者定義函數的說明文件集。<br /><br /> 傳回**VT_NULL** MDX 函數。|  
|**HELP_CONTEXT**|**DBTYPE_I4**||(選擇性) 傳回這個函數的說明內容識別碼。|  
|**OBJECT**|**DBTYPE_WSTR**||(選擇性) 屬性所套用至的物件類別的一般名稱。 例如，資料列集對應至 < l >。成員函式會傳回"**層級**"。<br /><br /> 傳回**VT_NULL**使用者定義函式或非屬性的 MDX 函數。|  
|**標題**|**DBTYPE_WSTR**||函數的顯示標題。|  
  
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
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  