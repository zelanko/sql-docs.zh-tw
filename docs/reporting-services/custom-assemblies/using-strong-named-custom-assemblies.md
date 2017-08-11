---
title: "使用強式名稱自訂組件 |Microsoft 文件"
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
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: cf8ee5462bd75ab82ea4296a5b71136cb2eb9ee9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="using-strong-named-custom-assemblies"></a>使用強式名稱自訂組件
  強式名稱會識別組件，並且含括組件的文字名稱、四部分的版本號碼、文化特性資訊 (若有提供)、公用金鑰，以及儲存在組件資訊清單中的數位簽章。 強式名稱可唯一識別 Common Language Runtime (CLR) 並確保二進位的完整性。  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>使用 AllowPartiallyTrustedCallersAttribute  
 若要搭配報表使用強式名稱組件，您必須允許強式名稱組件由部分信任程式碼使用的組件呼叫**AllowPartiallyTrustedCallers**屬性。 您可以使用**AllowPartiallyTrustedCallersAttribute** ，允許由報表設計師或報表運算式中的報表伺服器呼叫強式名稱的組件。 若要允許部分信任的程式碼呼叫強式名稱組件，請將下列組件層級屬性加入組件屬性檔。  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute**是由強式名稱組件的組件層級套用時才有效。 如需有關在組件層級套用屬性的詳細資訊，請參閱 < 套用屬性 > 中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件。  
  
> [!CAUTION]  
>  當**AllowPartiallyTrustedCallersAttribute**沒有、 預設**FullTrustLinkDemand**安全性檢查，將會避免、 讓組件可從其他任何呼叫部分信任組件。 所有的安全性檢查都必須明確地陳述，包括類別層級或是方法層級宣告的安全性屬性。  
  
## <a name="see-also"></a>另請參閱  
 [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
