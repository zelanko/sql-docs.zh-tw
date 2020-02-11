---
title: 將報表連結至模型做為點選連結報表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- customizing clickthrough reports
- clickthrough reports, customizing
- clickthrough reports, templates
ms.assetid: 3af42de3-67ef-41c2-bc8a-7045baec6f63
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 45b7695a9cd259d10155036ce1f9367a71e2fe72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108365"
---
# <a name="link-a-report-to-a-model-as-a-clickthrough-report"></a>將報表連結至模型以做為點選連結報表
  如果不使用預設點選連結報表範本，您可以建立報表產生器報表，然後將它連結至報表模型中的特定實體。 當檢視報表的人按一下主報表中的互動式資料時，此報表就會顯示為點選連結報表。 若要將報表連結至實體，請使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表管理員。  
  
> [!IMPORTANT]  
>  報表中使用的主要實體或基底實體，必須與連結報表的實體相同。  
  
### <a name="to-start-report-manager-from-a-browser"></a>若要從瀏覽器啟動報表管理員  
  
1.  開啟 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 6.0 或更新版本。  
  
2.  在網頁瀏覽器的網址列中，輸入報表管理員 URL。 根據預設，URL 為 HTTP://\<*ComputerName*>/reports。  
  
### <a name="to-create-a-customized-clickthrough-report"></a>建立自訂點選連結報表  
  
1.  導覽至您要加入自訂點選連結報表的目標報表模型。  
  
2.  按兩下報表模型。  
  
3.  按一下 **[Clickthrough]**。  
  
4.  選取您要附加自訂點選連結報表的目標實體。  
  
    > [!NOTE]  
    >  這個實體必須與自訂點選連結報表的基礎實體相同。  
  
5.  若要在按一下所選實體的單一執行個體時顯示自訂報表，按一下單一執行個體報表的 **[瀏覽]** 按鈕。  
  
     -或-  
  
     若要在按一下所選實體的多個執行個體時顯示自訂報表，按一下多個執行個體報表的 **[瀏覽]** 按鈕。  
  
6.  選取報表，然後按一下 **[確定]**。  
  
7.  按一下 [套用]  。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSRS&#41;的點選連結報表](reports/clickthrough-reports-ssrs.md)  
  
  
