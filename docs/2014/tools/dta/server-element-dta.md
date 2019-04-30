---
title: Server 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6c73db809e81cc9b6d1ee182227078a83688384
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273426"
---
# <a name="server-element-dta"></a>Server 元素 (DTA)
  包含您要微調的資料庫所在之伺服器的識別資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
    <Server>  
    ...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|(必要) 每個 `DTAInput` 元素出現一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素 &#40;DTA&#41;](dtainput-element-dta.md)|  
|**子元素**|[伺服器的 Name 元素 &#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [伺服器的 Database 元素 &#40;DTA&#41;](database-element-for-server-dta.md)|  
  
## <a name="remarks"></a>備註  
 您可以指定只有一個`Server`項目`DTAInput`項目。 在 DTA XML 結構描述中，這個元素是 **ServerDetailsTypecomplexType** 名稱。 請勿混淆這個 `Server` 元素和 `Configuration` 元素的子元素。 如需詳細資訊，請參閱[組態的 Server 元素 &#40;DTA&#41;](server-element-for-configuration-dta.md)。  
  
## <a name="example"></a>範例  
 下列範例顯示如何在 SERVER001 的 **AdventureWorks** 資料庫中，指定 **Sales.SalesPerson** 資料表：  
  
```xml  
<Server>  
  <Name>SERVER001</Name>  
  <Database>  
    <Name>AdventureWorks</Name>  
    <Schema>  
      <Name>Sales</Name>  
      <Table>  
        <Name>SalesPerson</Name>  
      </Table>  
    </Schema>  
  </Database>  
</Server  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
