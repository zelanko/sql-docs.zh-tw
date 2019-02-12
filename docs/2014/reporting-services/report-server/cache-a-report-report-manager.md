---
title: 快取報表 (報表管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- cached reports [Reporting Services]
- schedules [Reporting Services], report expiration
- expiration [Reporting Services]
ms.assetid: 723d1cb0-c2e7-4763-8690-a6a7a8bbbb90
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 4269c5219dc52df82f46f1d495d895321fc6f276
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023589"
---
# <a name="cache-a-report-report-manager"></a>快取報表 (報表管理員)
  改善效能的其中一種方式就是設定報表的快取屬性。 快取報表時，系統就會在一段短時間內儲存已轉譯報表的副本。 要求報表的第一位使用者必須等候所有處理都完成，然後才能檢視該報表。 在快取期間內要求該報表的後續使用者可以立即檢視報表，因為處理已經進行了。  
  
 您可以快取的報表類型有所限制。 例如，如果報表輸出會因使用者識別而不同，或者資料是使用要求報表之使用者的安全性 Token 擷取的，系統就無法快取該報表。 如需詳細資訊，請參閱 [快取報表 &#40;SSRS&#41;](caching-reports-ssrs.md)。  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>若要排程快取報表的逾期  
  
1.  啟動[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  在報表管理員中，導覽至 **[內容]** 頁面。 導覽至您想要設定快取屬性的報表、將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]**。  
  
4.  在左框架內，按一下 [處理選項]。  
  
5.  在頁面上，選取 [永遠以最新的資料執行此報表]。  
  
6.  選取下列兩個快取選項的其中之一，並設定逾期如下：  
  
    -   若要設定快取副本在特定時間週期之後過期，請按一下 **[快取報表的暫存副本。報表副本會在下列分鐘數後過期]**。 輸入報表過期的分鐘數。  
  
    -   若要設定快取副本依據排程過期，請按一下 [快取報表的暫存副本。**在下列排程上使報表的副本過期]。** 按一下 [設定]，或選取共用排程來控制報表逾期  
  
7.  按一下 **[套用]**。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表處理屬性](set-report-processing-properties.md)   
 [快取報表 &#40;SSRS&#41;](caching-reports-ssrs.md)  
  
  
