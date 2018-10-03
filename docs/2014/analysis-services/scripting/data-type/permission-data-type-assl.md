---
title: Permission 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8d12fb71a8ed19ca083e8ec506fba6338f6b58a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101939"
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
|基底資料類型|None|  
|衍生資料類型|[CubePermission](../objects/cubepermission-element-assl.md)， [DatabasePermission](../objects/databasepermission-element-assl.md)， [DimensionPermission](permission-data-type-assl.md)， [MiningModelPermission](../objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[註釋](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[描述](../properties/description-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名稱](../properties/name-element-assl.md)，[程序](../properties/process-element-assl.md)，[讀取](../properties/read-element-assl.md)， [ReadDefinition](../properties/readdefinition-element-assl.md)，[物件的 RoleID](../properties/roleid-element-assl.md)，[寫入](../properties/write-element-assl.md)|  
|衍生的元素|None|  
  
## <a name="remarks"></a>備註  
 `Permission` 做為抽象的基底類型衍生的權限類型的執行個體中使用數個[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 此資料類型在 DeploymentMode 值 2 (表格式伺服器模式) 下，擁有下列驗證。  
  
-   *處理程序*屬性預設值設為`False`，除非使用者具有**重新整理**權限。 為使用者**重新整理**權限*程序*屬性值設為`True`。  
  
-   *ReadDefinition*屬性值設為`None`; 任何其他值會產生錯誤。  
  
-   *讀取*屬性值設為`Allowed`的使用者**使用者**權限以及`None`時將使用者指派給**重新整理**權限; 如果使用者同時具有**使用者**並**重新整理**權限，則此屬性設定為`Allowed`。 使用者若是具有系統管理權限，屬性值會設為 `Allowed`。  
  
-   *撰寫*屬性值設為`None`; 任何其他值會產生錯誤。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
