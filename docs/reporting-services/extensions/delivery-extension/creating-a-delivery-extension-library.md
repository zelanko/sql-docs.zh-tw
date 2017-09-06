---
title: "建立傳遞延伸模組程式庫 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 63b32f93-4bab-4b07-bd72-39a47aca1cda
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bcfb5b69df148108531e9e5b843f127af0e3fbb4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---
# <a name="creating-a-delivery-extension-library"></a>建立傳遞延伸模組程式庫
  每個您建立的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組都應該指派到唯一的命名空間，並內建於程式庫或是組件檔中。 命名空間的正確名稱並不重要，但是它必須是唯一且未與其他延伸模組共用。 您應該為公司的傳遞延伸模組建立自己的唯一命名空間。  
  
 下列範例示範開始 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組的程式碼，這是使用包含傳遞介面與任何公用程式類別的命名空間。  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 編譯 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組時，您必須提供 Microsoft.ReportingServices.Interfaces.dll 的參考給編譯器，因為其中包含傳遞延伸模組介面與類別。 需要 <xref:Microsoft.ReportingServices.Interfaces> 命名空間實作 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面、<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 介面等等。 例如，如果所有包含程式碼來實作[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]以 C# 撰寫的傳遞延伸模組都在單一目錄中並且副檔名為.cs，會從要編譯儲存在 CompanyName.ExtensionName.dll 中的檔案該目錄發出下列命令。  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 下列程式碼範例顯示的命令，則會使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]副檔名的檔案。 為.vb 之  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  您也可以使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 來設計、開發和建立傳遞延伸模組。 如需有關在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中開發組件的詳細資訊，請參閱 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
