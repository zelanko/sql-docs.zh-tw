---
title: 變更報表伺服器上的時區和時鐘設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- time zones [Reporting Services]
- clocks [Reporting Services]
- schedules [Reporting Services], clock settings
- schedules [Reporting Services], time zones
ms.assetid: 69a19468-baa1-40f6-b158-8afdab0f8968
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f8eee5dfea43865ad51580cbcdb105299f8edc37
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960824"
---
# <a name="change-time-zones-and-clock-settings-on-a-report-server"></a>變更報表伺服器上的時區和時鐘設定
  報表伺服器會永遠使用所安裝之電腦的本地時間。 您無法設定使用不同時區。 如果用戶端應用程式指向不同時區的報表伺服器，就會使用該報表伺服器的時區來執行排程作業。 在報表管理員和 SharePoint 管理頁面中，每個排程頁面都會顯示時區設定，好讓您確實知道已排程作業將發生的時候。 例如，用來建立自訂排程的頁面將會標示「時間是以 (UTC-08:00) 太平洋時間 (美國和加拿大) 格式表示」。  
  
## <a name="changing-the-time-zone-native-mode"></a>變更時區 (原生模式)  
 如果您變更了主控報表伺服器之電腦上的時區，就必須重新啟動報表伺服器服務，才能使時區變更生效。  
  
 現有報表記錄快照集的時間戳記值會與新的時區設定進行同步處理。 若您在上午 9:00 產生一個報表記錄快照集，然後將時區重設為早一個時區，則已產生快照集上的時間戳記將會從上午 9:00 變成上午 10:00。  
  
 排程會仍保留現有設定，除非有對應到新的時區。 例如，若排程在太平洋標準時間上午 2:00 執行， 而您將時區變更為東澳標準時間，則排程就會在東澳標準時間 上午 2:00 執行。  
  
 屬性時間戳記值 (例如，資料夾或連結報表項目的建立時間) 則不會與新的時區設定進行同步處理。 如果您在 6 月 25 日的上午 9:00 建立一個項目，然後重設時區或時鐘，則時間戳記仍會保留為 6 月 25 日的上午 9:00。  
  
## <a name="changing-the-time-zone-sharepoint-mode"></a>變更時區 (SharePoint 模式)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式的時區組態會當做 SharePoint 地區設定的一部分來管理。 如需詳細資訊，請參閱[區域設定 (SharePoint Server 2010 (https://technet.microsoft.com/library/cc824907.aspx)](https://technet.microsoft.com/library/cc824907.aspx)。  
  
## <a name="changing-the-clock-settings"></a>變更時鐘設定  
 變更電腦時鐘不會影響現有的時間戳記值 (例如，若您將時間往前調一小時，報表記錄快照集的時間戳記並不會變更)。 在排程與傳遞處理器使用新的設定以前，可能會有 10 秒的延遲。 如果您有在組態檔中修改輪詢間隔設定，實際的延遲就會因設定而異。  
  
## <a name="see-also"></a>另請參閱  
 [啟動與停止 Report Server 服務](../report-server/start-and-stop-the-report-server-service.md)   
 [排程](schedules.md)  
  
  
