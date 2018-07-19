---
title: 疑難排解報表組件 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d9fe1932-46e7-421b-a8a9-4c54d9576e94
caps.latest.revision: 6
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ce472be61a85aa1adfad529c38cd74c8dcd9d17a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148569"
---
# <a name="troubleshoot-report-parts-report-builder-and-ssrs"></a>疑難排解報表組件 (報表產生器及 SSRS)
  這些提示可在您處理報表組件時協助您。  
  
## <a name="why-do-my-co-worker-and-i-see-different-instances-of-the-same-report-part-when-we-search-for-it"></a>為什麼我的同事和我在搜尋報表組件時看到相同報表組件的不同執行個體？  
 在報表伺服器或與報表伺服器整合的 SharePoint 網站上，可以有單一報表組件的多個執行個體，而且所有執行個體都有相同的全域唯一識別碼 (GUID)。 只有最新的執行個體會顯示在搜尋結果的清單中。 在某些情況下，單一報表組件的不同執行個體可以擁有不同的權限。 如果您的同事和您在伺服器上具有不同的權限，您不會看到相同的執行個體。 例如，假設某個報表組件的多個複本 (全部擁有相同的 GUID) 都儲存在 SharePoint 整合模式下，報表伺服器上的不同資料夾中。 如果資料夾有不同的權限，則這些資料夾中的報表組件也都會有不同的權限。  
  
 若要查看您和您的同事所具有的權限為何，請詢問報表伺服器管理員。  
  
## <a name="when-i-search-for-report-parts-that-i-uploaded-to-a-sharepoint-server-i-do-not-see-them-why-not"></a>當我搜尋上傳至 SharePoint 伺服器的報表組件時，看不到這些報表組件。 為什麼看不到呢？  
 您已經手動上傳至 SharePoint 文件庫的報表組件 (而非使用報表產生器發行的報表組件) 可能不會顯示在報表組件庫中。 用於組件庫搜尋的報表伺服器可能需要與 SharePoint 文件庫的內容同步處理。 如需詳細資訊，請參閱 <<c0> [ 啟動報表伺服器檔案同步處理功能，在 SharePoint 管理中心內](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][線上叢書 》](http://go.microsoft.com/fwlink/?LinkId=154888) msdn.microsoft.com 上。  
  
## <a name="why-cant-others-see-the-image-in-their-reports"></a>為什麼其他人的報表中看不到影像？  
 如果您發行的報表組件是影像檔案的連結，該報表組件實際上就只是一個連結。 如果其他人將影像報表組件加入到報表時看不到影像，則表示他們可能不具備您所連結之影像的權限。  
  
 這種情況有幾種可能的解決方案：  
  
-   讓影像檔案變成報表組件，而不要讓影像檔案的連結變成報表組件。  
  
-   將影像檔案移到其他人具有權限的位置。  
  
-   要求報表伺服器管理員變更權限。  
  
## <a name="why-do-i-get-a-circular-reference-error-message-when-i-try-to-publish-my-report-part"></a>當我嘗試發行報表組件時，為什麼會出現「循環參考」錯誤訊息？  
 如果報表項目有循環參考，您將無法將它們發行為報表組件。 例如，報表項目會指向資料集，再依序指向參數。 參數也會依序指向資料集。 您必須先刪除其中一個參考，然後才可以發行報表組件。  
  
## <a name="see-also"></a>另請參閱  
 [報表組件&#40;報表產生器及 SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  
