---
title: 建立資料處理延伸模組程式庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 82f4b71b-dd39-467d-8d8c-6771eb2b12de
caps.latest.revision: 39
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 88acc6f623c3aefa398d4dcd4847e2cf00cbb19e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33016155"
---
# <a name="creating-a-data-processing-extension-library"></a>建立資料處理延伸模組程式庫
  每個您建立的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組都應該指派到唯一的命名空間，並內建於程式庫或是組件檔中。 命名空間的正確名稱並不重要，但是它必須是唯一且未與其他延伸模組共用。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 隨附的資料處理延伸模組使用命名空間 <xref:Microsoft.ReportingServices.DataProcessing>。 您應該為公司的資料處理延伸模組建立自己的唯一命名空間。  
  
 下列範例示範開始 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組的程式碼，這是使用包含資料處理介面與任何公用程式類別的命名空間。  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.DataProcessing  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.DataProcessing;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 編譯 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組時，您必須提供 Microsoft.ReportingServices.Interfaces.dll 的參考給編譯器，因為其中包含資料處理延伸模組介面。 需要 <xref:Microsoft.ReportingServices.DataProcessing> 命名空間實作資料處理延伸模組介面，而且需要 <xref:Microsoft.ReportingServices.Interfaces> 命名空間實作 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面。 例如，如果所有包含程式碼以實作用 C# 撰寫的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組之檔案，都在單一目錄中並且副檔名為 .cs，則會從該目錄發出下列命令，以編譯儲存在 CompanyName.ExtensionName.dll 中的檔案。  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 下列程式碼範例示範將用於副檔名為 .vb 之 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 檔案的命令。  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  您也可以使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 來設計、開發和建立資料處理延伸模組。 如需有關在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中開發組件的詳細資訊，請參閱 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
