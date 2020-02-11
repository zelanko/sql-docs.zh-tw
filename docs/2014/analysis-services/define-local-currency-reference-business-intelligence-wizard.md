---
title: 定義本地貨幣參考（商業智慧 Wizard） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.localcurrency.f1
ms.assetid: 74993b0d-dfca-476b-acba-d66c593680a5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 558e2c7d62edcb9fb314b49d41fd7bd15413218d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082182"
---
# <a name="define-local-currency-reference-business-intelligence-wizard"></a>定義本地貨幣參考 (商業智慧精靈)
  使用 [定義本地貨幣參考]**** 頁面，即可定義貨幣轉換功能的本地貨幣，這會涵蓋 [選取轉換類型]**** 頁面上指定的多對多或多對一轉換類型。 本地貨幣為 **[選取量值]** 頁面中，選取之量值用於儲存交易的貨幣。  
  
> [!NOTE]  
>  如果 [商業智慧精靈] 是從 [維度設計師] 啟動，或是在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中方案總管的某維度上按一下滑鼠右鍵來啟動，則不會出現此頁面。 如果選取 [選取轉換類型]**** 頁面上的 [一對多]****，這個頁面也不會出現。  
  
## <a name="options"></a>選項。  
 **事實資料表中的識別碼**  
 選取即可指定屬性，在包含 [選取量值]**** 頁面上所選取量值的事實資料表所參考的貨幣維度中，提供本地貨幣的貨幣識別碼 （其中一個`Type`屬性設定為*currency*的貨幣維度）。  
  
 當交易自行決定該交易的本地貨幣時，請使用此選項。 例如[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，在範例資料庫[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]中，[網際網路銷售] 量值群組與 [貨幣] 維度具有一般維度關聯性。 該量值群組的事實資料表包含外部索引鍵資料行，此資料行參考該維度之維度資料表中的貨幣識別碼。  
  
 **事實資料所參考的貨幣維度與屬性**  
 在貨幣維度中選取貨幣屬性，其成員代表本地貨幣的貨幣識別碼。 （貨幣屬性是其`Type`屬性設為*currency*的屬性）。  
  
> [!NOTE]  
>  若未選取 [事實資料表中的識別碼]**** 選項，則無法使用此選項。  
  
 **維度資料表中的屬性**  
 選取即可從與量值群組相關的維度中指定屬性，該量值群組包含本地貨幣的貨幣識別碼。  
  
 當交易與其他商務實體 (例如位置) 間的關聯性，會決定該交易的本地貨幣時，請使用此選項。 例如，在[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]範例資料庫[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]中，財務報表量值群組會透過組織維度，與貨幣維度有參考的維度關聯性。 也就是說，財務報表量值群組的事實資料表中包含的外部索引鍵資料行，參考到組織維度之維度資料表中的成員。 而組織維度的維度資料表包含外部索引鍵資料行，此資料行參考貨幣維度之維度資料表中的貨幣識別碼。  
  
 **參考貨幣的維度屬性**  
 在維度中選取屬性，其成員參考本地貨幣的貨幣識別碼。  
  
> [!NOTE]  
>  若未選取 [維度資料表中的屬性]**** 選項，則無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [商業智慧 Wizard F1 說明](business-intelligence-wizard-f1-help.md)   
 [Cube 設計工具 &#40;Analysis Services-多維度資料&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [維度設計師 &#40;Analysis Services 多維資料&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
