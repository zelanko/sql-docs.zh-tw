---
title: 疑難排解圖表 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 01/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f74e09afc4be0bf5297f0c7e6e4026fbf57e0dae
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43264568"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>疑難排解圖表 (報表產生器及 SSRS)
  使用圖表時，這些問題很有協助。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>為什麼我的圖表計數不會針對值軸上的值加總？  
 大多數的圖表類型都需要沿著值軸 (通常為 Y 軸) 放置數值，才能正確繪製。 如果值欄位的資料類型為 **String**，即使欄位中有數字，圖表也無法顯示數值。 但是，圖表會顯示在該欄位中包含值之資料列總數的計數。 若要避免發生這個問題，請確定您用於值數列的欄位具有數值資料類型，而不是包含格式化數字的字串。  

## <a name="need-more-help"></a>需要其他協助嗎？  
   
  請嘗試：  
 * Stack Overflow 上的 [SQL Server Reporting Services](https://stackoverflow.com/questions/tagged/reporting-services)  
 * 在 [Microsoft SQL Server UserVoice](https://feedback.azure.com/forums/908035-sql-server) 記錄問題或建議。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
