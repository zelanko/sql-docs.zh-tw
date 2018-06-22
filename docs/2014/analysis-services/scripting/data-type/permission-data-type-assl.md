---
title: Permission 資料類型 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Permission Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Permission
helpviewer_keywords:
- Permission data type
ms.assetid: 5f309544-59f8-4432-b1eb-b7c1a049f8df
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ff5fb67e4f7989fb329e60a106ea8e6d0c734c97
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022714"
---
# <a name="permission-data-type-assl"></a>Permission 資料類型 (ASSL)
  定義代表個別權限之相關資訊的抽象基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Permission>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <RoleID>...</RoleID>  
   <Description>...</Description>  
   <Process>...</Process>  
   <ReadDefinition>...</ReadDefinition>  
   <Read>...</Read>  
   <Write>...</Write>  
   <Annotations>...</Annotations>  
</Permission>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[CubePermission](../objects/cubepermission-element-assl.md)， [DatabasePermission](../objects/databasepermission-element-assl.md)， [DimensionPermission](permission-data-type-assl.md)， [MiningModelPermission](../objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註解](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[描述](../properties/description-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名稱](../properties/name-element-assl.md)，[程序](../properties/process-element-assl.md)，[讀取](../properties/read-element-assl.md)， [ReadDefinition](../properties/readdefinition-element-assl.md)， [RoleID](../properties/roleid-element-assl.md)，[寫入](../properties/write-element-assl.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 `Permission` 做為一些衍生權限類型的執行個體中使用的抽象基底類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 此資料類型在 DeploymentMode 值 2 (表格式伺服器模式) 下，擁有下列驗證。  
  
-   *處理序*屬性預設值設為`False`，除非使用者具有**重新整理**權限。 具有使用者**重新整理**權限*程序*屬性值設為`True`。  
  
-   *ReadDefinition*屬性值設為`None`; 任何其他值會產生錯誤。  
  
-   *讀取*屬性值設為`Allowed`的使用者使用**使用者**權限以及`None`當將使用者指派給**重新整理**權限; 如果使用者同時具有**使用者**和**重新整理**權限，則此屬性設定為`Allowed`。 使用者若是具有系統管理權限，屬性值會設為 `Allowed`。  
  
-   *寫入*屬性值設為`None`; 任何其他值會產生錯誤。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  