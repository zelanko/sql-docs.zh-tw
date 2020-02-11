---
title: 建立父子式類型維度的財務帳戶 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], account
- account dimensions [Analysis Services]
- adding account intelligence
- account intelligence [Analysis Services]
ms.assetid: 2ba74e81-5b4b-407e-acdf-deb2f6accf0a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28a7cf6b3a712144daead54d521fb3cc6936c99e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075914"
---
# <a name="create-a-finance-account-of-parent-child-type-dimension"></a>建立父子式類型維度的財務帳戶
  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，帳戶類型維度是其屬性代表財務報表用途之帳戶圖表的維度。  
  
 帳戶維度可讓您選擇性地管理帳戶經過一段時間之後的彙總行為。 帳戶維度也可讓您使用標準機制，來解決通常發生在處理財務資料之商業智慧方案中的大部份非標準彙總問題。 如果您沒有這樣的標準機制，要解決這些非標準彙總問題，您需要自訂積存公式、導出成員或多維度運算式 (MDX) 指令碼。  
  
 若要將維度識別為帳戶維度，請將維度的 `Type` 屬性設定為 `Accounts`。  
  
## <a name="dimension-structure"></a>維度結構  
 帳戶維度至少包含兩個屬性：  
  
-   索引鍵屬性-識別帳戶維度之維度資料表中個別帳戶的屬性。  
  
-   帳戶屬性-描述帳戶如何以階層方式排列在帳戶維度中的父屬性。  
  
     若要將屬性 (Attribute) 識別為帳戶屬性，請將屬性 (Attribute) 的 `Type` 屬性 (Property) 設定為 `Account` 和 `Usage` 屬性 (Property) 設定為 `Parent`。  
  
 帳戶維度可選擇性地包含下列屬性：  
  
-   帳戶類型屬性-定義維度中每個帳戶之帳戶類型的屬性。 帳戶類型屬性的成員名稱會對應到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫或專案之已定義的帳戶類型，並指出 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 針對那些帳戶使用的彙總函式。 您也可以使用一元運算子或自訂積存公式來決定帳戶屬性的彙總行為，但帳戶類型可讓您輕易地將一致的行為套用至帳戶的圖表中，而不需要變更基礎關聯式資料庫。  
  
     若要識別帳戶類型屬性 (Attribute)，請將屬性 (Attribute) 的 `Type` 屬性 (Property) 設定為 `AccountType`。  
  
-   帳戶名稱屬性-用於報告用途的屬性。 若要識別帳戶名稱屬性 (Attribute)，請將屬性 (Attribute) 的 `Type` 屬性 (Property) 設定為 `AccountName`。  
  
-   帳戶號碼屬性-用於報告用途的屬性。 若要識別帳戶號碼屬性 (Attribute)，請將屬性 (Attribute) 的 `Type` 屬性 (Property) 設定為 `AccountNumber`。  
  
 如需屬性類型的詳細資訊，請參閱 [設定屬性類型](attribute-properties-configure-attribute-types.md)。  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>使用商業智慧精靈加入帳戶智慧  
 在定義帳戶維度並將該維度加入至 Cube 之後，您可以使用商業智慧精靈來將帳戶智慧功能 (例如識別和對應帳戶類型) 加入至維度。 如需詳細資訊，請參閱 [將帳戶智慧加入至維度中](bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [商業智慧 Wizard F1 說明](../business-intelligence-wizard-f1-help.md)   
 [維度類型](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
