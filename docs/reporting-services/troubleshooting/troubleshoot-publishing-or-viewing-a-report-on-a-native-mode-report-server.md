---
title: "疑難排解發行或原生模式報表伺服器上檢視報表 |Microsoft 文件"
ms.custom: 
ms.date: 02/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: df7720a1-d178-45bb-8d6f-63e208cae7fe
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c0c974553c7c05fdbf853be1a2028c30eaffc3b2
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="troubleshoot-publishing-or-viewing-a-report-on-a-native-mode-report-server"></a>在原生模式報表伺服器上疑難排解發行或檢視報表
  
  
  
當您發行或上傳報表至設為原生模式的報表伺服器時，可能會看到在報表伺服器上檢視報表的特定問題。 您可以使用本主題來協助疑難排解這些問題。   
  
## <a name="why-am-i-being-prompted-for-credentials-when-i-publish-a-report"></a>為什麼當我發行報表時，出現要求認證的提示？  
若要將報表部署到報表伺服器，您必須指定伺服器的位址。 您可能會看到 [Reporting Services 登入] 對話方塊，提示您輸入認證。   
  
報表伺服器名稱未正確指定  
  
  
當您部署報表至原生模式的報表伺服器時，常見的錯誤是指定報表資料夾的名稱，而非報表伺服器的名稱。   
  
確認報表伺服器 URL 是報表伺服器的位址 (例如 `http://localhost/reportserver`)，而非報表管理員虛擬目錄的位址 (例如 `http://localhost/reports`)。 如果您已經為報表伺服器指定了與預設通訊埠編號 80 不同的通訊埠編號，您必須在報表伺服器位址中指定它 (例如 `http://localhost:81/reportserver`)。   
  
 ## <a name="nothing-happens-when-i-toggle-items-in-my-published-report"></a>當我在已發行的報表中切換項目時，沒有反應。  
  在本機預覽中檢視報表時，您可以切換報表中的項目，並加以顯示或隱藏。 當報表發行至報表伺服器後，重新檢視報表時，切換項目會失去作用。   
  
\<報表伺服器名稱 > 包含底線 (_)  
  
如果報表執行時沒有錯誤，但是切換項目沒有作用 (例如，您按一下展開按鈕 (+) 但沒有反應)，請檢查主控報表伺服器之電腦的名稱。 如果電腦名稱包含底線，切換項目會沒有作用。 這是已知的問題。 沒有因應措施。   
  
若要執行可以切換項目報表，就必須使用名稱中不包含底線字元的電腦。  
  
## <a name="images-and-charts-do-not-load-when-i-use-run-as-and-a-browser-to-run-my-report"></a>使用執行身分和瀏覽器來執行報表時，影像和圖表未載入。  
當您在不同的安全性內容下執行報表管理員時，可能看不到報表中的所有報表項目。   
  
### <a name="insufficient-permissions-on-internet-temporary-file-folders"></a>Internet Temporary File 資料夾的權限不足  
  
在某些情況下，當您使用報表管理員檢視已發行的報表時，可能看不到其中包含的圖表或影像。 例如，當您使用 Microsoft Windows **Run As** 命令檢視使用不同安全性內容的報表時，對於報表伺服器將圖表和影像快取為暫存 Internet 檔案時所使用的資料夾，您可能沒有存取權限。   
  
請確認您有權限可以存取包含快取檔案的資料夾。   
    
## <a name="see-also"></a>請參閱＜  
[Reporting Services 和 Power View 的瀏覽器支援](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[錯誤和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[搭配 Reporting Services 報表為資料擷取問題疑難排解](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[為 Reporting Services 訂閱與傳遞疑難排解](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


