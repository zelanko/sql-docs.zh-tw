---
title: 快取頁面、共用資料集（報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eac372e9-d2a1-48a8-bbe5-09d101df16ea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ae18d021465a7d14ea22b56534ea48ac316154c2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109905"
---
# <a name="caching-page-shared-datasets-report-manager"></a>快取頁面、共用資料集 (報表管理員)
  使用 [快取屬性] 頁面，即可設定共用資料集的快取選項。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需版本支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱[SQL Server 2014 版本支援的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面中導覽至這個位置。  
  
### <a name="to-open-the-caching-properties-page-for-a-shared-dataset"></a>開啟共用資料集的快取屬性頁面  
  
1.  開啟報表管理員，然後找出您想要設定共用資料集屬性的報表。  
  
2.  指向共用資料集，然後按下拉式箭號。  
  
3.  在下拉式清單中，按一下 **[管理]**， 報表的 [一般屬性] 頁面隨即開啟。  
  
4.  按一下 **[快取]** 索引標籤。  
  
## <a name="options"></a>選項。  
 **快取共用資料集**  
 當使用者第一次開啟使用此共用資料集的報表時，會在快取中放置資料的暫存副本。 在快取期間內執行此報表的後續使用者都會收到快取的資料副本。 快取通常會改善效能，因為資料是從快取傳回，而非再次執行資料集查詢。  
  
 **快取於這個分鐘數後過期**  
 指定要儲存快取之資料副本的分鐘數。 一旦暫存副本過期，就不會再從快取中傳回資料。 使用者下次開啟使用此共用資料集的報表時，會執行資料集查詢，然後報表伺服器會將重新整理過的資料副本放回快取中。  
  
 **快取於下列排程時到期**  
 排程快取的資料不再有效並從快取移除的時間。 排程可以是共用的排程或是特屬目前共用資料集的排程。  
  
 **資料集特定排程**  
 指定僅供此資料集使用的排程。  
  
 **共用排程**  
 指定報表、訂閱及其他共用資料集所共用的排程。  
  
 **套用**  
 儲存您的變更。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [&#40;SSRS&#41;快取共用資料集](report-server/cache-shared-datasets-ssrs.md)   
 [排程](subscriptions/schedules.md)  
  
  
