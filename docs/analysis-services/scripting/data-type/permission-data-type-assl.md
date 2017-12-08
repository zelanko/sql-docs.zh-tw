---
title: "Permission 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Permission Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Permission
helpviewer_keywords: Permission data type
ms.assetid: 5f309544-59f8-4432-b1eb-b7c1a049f8df
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6dc58a84e1e93f7d309f10449eb27740e65f2b4d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
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
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)， [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)， [DimensionPermission](../../../analysis-services/scripting/data-type/dimensionpermission-data-type-assl.md)， [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[程序](../../../analysis-services/scripting/properties/process-element-assl.md)，[讀取](../../../analysis-services/scripting/properties/read-element-assl.md)， [ReadDefinition](../../../analysis-services/scripting/properties/readdefinition-element-assl.md)， [RoleID](../../../analysis-services/scripting/properties/roleid-element-assl.md)，[寫入](../../../analysis-services/scripting/properties/write-element-assl.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 **權限**做一些衍生權限類型的執行個體中使用的抽象基底類型為[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 此資料類型在 DeploymentMode 值 2 (表格式伺服器模式) 下，擁有下列驗證。  
  
-   *處理序*屬性預設值設為**False**，除非使用者具有**重新整理**權限。 具有使用者**重新整理**權限*程序*屬性值設為**True**。  
  
-   *ReadDefinition*屬性值設為**無**; 任何其他值會產生錯誤。  
  
-   *讀取*屬性值設為**允許**的使用者使用**使用者**權限以及**無**當將使用者指派給**重新整理**權限; 如果使用者同時具有**使用者**和**重新整理**權限，則此屬性設定為**允許**。 屬性值設定為具有系統管理權限的使用者**允許**。  
  
-   *寫入*屬性值設為**無**; 任何其他值會產生錯誤。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>請參閱＜  
 [Role 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
