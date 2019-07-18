---
title: 建立及管理原生模式報表伺服器的訂用帳戶 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], managing
ms.assetid: 7f46cbdb-5102-4941-bca2-5e0ff9012c6b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d6f18ff05cf6283e4358e8f8afd76a5858b0b41a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109602"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>建立及管理原生模式報表伺服器的訂閱
  此章節包含有關訂閱處理、監視和控制的主題。 訂閱管理在標準訂閱和資料驅動訂閱不同。 標準訂閱通常為使用者所擁有並管理。 相對地，資料驅動訂閱通常由報表伺服器管理員建立和維護。  
  
 訂閱與傳遞功能預設是啟用的 (電子郵件傳遞需要先進行設定，然後才能使用)。 預設傳遞延伸模組包括報表伺服器電子郵件和檔案共用傳遞。 除非您建立或安裝自訂的傳遞延伸模組，否則原生模式報表伺服器上的訂閱只能使用這些散發方法。  
  
## <a name="permissions-for-subscribing-to-reports-on-a-native-mode-report-server"></a>訂閱原生模式報表伺服器之報表的權限  
 視您使用角色的方式而定，您可以藉由針對不同角色啟用或停用訂閱工作，提供訂閱功能給選取的使用者群組。 訂閱功能會透過兩個工作提供給使用者：  
  
-   「管理個別訂閱」工作可以讓使用者建立、修改及刪除特定報表的訂閱。 在預先定義的角色中，這項工作屬於瀏覽器和報表產生器角色的一部分。 包含這個工作的角色指派，允許使用者只管理自己所建立的訂閱。  
  
-   「管理所有訂閱」工作可以讓使用者存取和修改所有的訂閱。 要建立資料驅動訂閱需要這個工作。 在預先定義的角色中，只有內容管理員角色包含這項工作。  
  
## <a name="disabling-subscriptions"></a>停用訂閱  
 若要讓使用者無法建立訂閱，請從角色中清除「管理個別訂閱」工作。 當您移除這個工作後，[訂閱] 頁面就無法使用。 在報表管理員中，即使 [我的訂閱] 頁面原先含有訂閱，此時也會顯示空白 (無法刪除這個頁面)。 移除訂閱相關的工作會讓使用者無法建立與修改訂閱，但是不會刪除現有的訂閱。 現有的訂閱仍會繼續執行，直到您刪除這些訂閱為止。 如需有關刪除訂用帳戶的詳細資訊，請參閱[建立、 修改和刪除標準訂用帳戶&#40;原生模式的 Reporting Services&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)。  
  
 若要停用報表伺服器上處理的訂用帳戶，您可以設定`ScheduleEventsAndReportDeliveryEnabled`屬性，以`False`中**Reporting Services 的介面區組態**facet 的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]原則為基礎的管理。 這樣做會讓所有排程的作業無法執行。 您無法單獨關閉報表伺服器的訂閱處理。  
  
 如需有關如何取消處理報表伺服器的訂用帳戶的指示，請參閱 <<c0> [ 管理執行的處理序](subscriptions/manage-a-running-process.md)。  
  
## <a name="disabling-delivery-extensions"></a>停用傳遞延伸模組  
 在報表伺服器上安裝的所有傳遞延伸模組都會提供給有權建立給定報表之訂閱的任何使用者。 系統會自動提供和設定下列傳遞延伸模組：  
  
-   Windows 檔案共用  
  
-   SharePoint 文件庫 (只能從與 SharePoint 整合模式報表伺服器整合的 SharePoint 網站使用)  
  
 您必須先設定電子郵件傳遞，然後才能使用它。 如果您沒有設定它，便無法使用它。 如需詳細資訊，請參閱 <<c0> [ 電子郵件傳遞設定報表伺服器&#40;SSRS 組態管理員&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。</c0>  
  
 如果您想要關閉特定延伸模組，可以在 RSReportServer.config 檔中移除延伸模組項目。 如需詳細資訊，請參閱 < [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md)並[電子郵件傳遞設定報表伺服器&#40;SSRS 組態管理員&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
 在您移除傳遞延伸模組之後，就無法再於報表管理員或 SharePoint 網站中使用它。 移除傳遞延伸模組可能會產生非使用中訂閱。 移除延伸模組之前，請務必刪除訂閱，或將它們設定為使用不同的傳遞延伸模組。  
  
## <a name="in-this-section"></a>本節內容  
 [使用我的訂閱](subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 說明如何使用 [我的訂閱] 頁面，以管理您所擁有的訂閱。  
  
 [暫停報表與訂閱處理](subscriptions/disable-or-pause-report-and-subscription-processing.md)  
 說明暫停報表處理的各種方式，例如使用角色指派或停用報表伺服器資源。  
  
 [控制報表散發](../../2014/reporting-services/control-report-distribution.md)  
 描述可用來控制報表散發的組態設定和傳遞選項。  
  
 [監視 Reporting Services 訂閱](subscriptions/monitor-reporting-services-subscriptions.md)  
 描述如何決定訂閱成功或失敗，以及在現有訂閱上所做報表變更的效果。  
  
## <a name="see-also"></a>另請參閱  
 [建立、 修改及刪除標準訂用帳戶&#40;Reporting Services 原生模式&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
