---
title: 快取頁面、 共用資料集 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eac372e9-d2a1-48a8-bbe5-09d101df16ea
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 65fe3e4979e620b3f49af5def2266c84e77cc616
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017880"
---
# <a name="caching-page-shared-datasets-report-manager"></a>快取頁面、共用資料集 (報表管理員)
  使用 [快取屬性] 頁面，即可設定共用資料集的快取選項。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面中導覽至這個位置。  
  
### <a name="to-open-the-caching-properties-page-for-a-shared-dataset"></a>開啟共用資料集的快取屬性頁面  
  
1.  開啟報表管理員，然後找出您想要設定共用資料集屬性的報表。  
  
2.  指向共用資料集，然後按下拉式箭號。  
  
3.  在下拉式清單中，按一下 **[管理]**， 報表的 [一般屬性] 頁面隨即開啟。  
  
4.  按一下 **[快取]** 索引標籤。  
  
## <a name="options"></a>選項。  
 **快取共用資料集**  
 當使用者第一次開啟使用此共用資料集的報表時，會在快取中放置資料的暫存副本。 在快取期間內執行此報表的後續使用者都會收到快取的資料副本。 快取通常會改善效能，因為資料是從快取傳回，而非再次執行資料集查詢。  
  
 **快取過期的分鐘數之後**  
 指定要儲存快取之資料副本的分鐘數。 一旦暫存副本過期，就不會再從快取中傳回資料。 使用者下次開啟使用此共用資料集的報表時，會執行資料集查詢，然後報表伺服器會將重新整理過的資料副本放回快取中。  
  
 **快取於下列排程時到期**  
 排程快取的資料不再有效並從快取移除的時間。 排程可以是共用的排程或是特屬目前共用資料集的排程。  
  
 **資料集特定排程**  
 指定僅供此資料集使用的排程。  
  
 **共用的排程**  
 指定報表、訂閱及其他共用資料集所共用的排程。  
  
 **套用**  
 儲存變更。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [快取共用資料集 &#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)   
 [排程](subscriptions/schedules.md)  
  
  
