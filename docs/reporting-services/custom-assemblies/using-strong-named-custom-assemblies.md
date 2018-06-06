---
title: 使用強式名稱自訂組件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: custom-assemblies
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 965c75a16e02d6561da2cf326a74f585e5e8be3a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-strong-named-custom-assemblies"></a>使用強式名稱自訂組件
  強式名稱會識別組件，並且含括組件的文字名稱、四部分的版本號碼、文化特性資訊 (若有提供)、公用金鑰，以及儲存在組件資訊清單中的數位簽章。 強式名稱可唯一識別 Common Language Runtime (CLR) 並確保二進位的完整性。  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>使用 AllowPartiallyTrustedCallersAttribute  
 若要在報表中使用強式名稱組件，則必須允許使用組件的 **AllowPartiallyTrustedCallers** 屬性之部分信任程式碼，呼叫強式名稱組件。 您可以使用 **AllowPartiallyTrustedCallersAttribute**，來允許報表設計師或是報表運算式中的報表伺服器呼叫強式名稱組件。 若要允許部分信任的程式碼呼叫強式名稱組件，請將下列組件層級屬性加入組件屬性檔。  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute** 只有在組件層級由強式名稱組件套用時才有效。 如需在組件層級套用屬性的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件集中的＜套用屬性＞。  
  
> [!CAUTION]  
>  當 **AllowPartiallyTrustedCallersAttribute** 存在時，會防止預設的 **FullTrustLinkDemand** 安全性檢查，以確定可從任何其他部分信任的組件呼叫組件。 所有的安全性檢查都必須明確地陳述，包括類別層級或是方法層級宣告的安全性屬性。  
  
## <a name="see-also"></a>另請參閱  
 [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
