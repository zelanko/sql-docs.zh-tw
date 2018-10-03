---
title: 保護主資料管理員 Web 應用程式的安全 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b3e74619a00e2f2e0db9529fc96ca93994f6895a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693376"
---
# <a name="secure-a-master-data-manager-web-application"></a>保護主資料管理員 Web 應用程式

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  您可以使用 HTTPS 保護 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式。  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式可以使用 HTTP 或 HTTPS，但不能同時使用兩者。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須是 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 安裝所在之 Web 伺服器的系統管理員。  
  
-   MDS 必須安裝在 Web 伺服器，而且 Web 應用程式必須存在。 如需詳細資訊，請參閱 [安裝 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md) 和 [建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)。  
  
### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>若要使用 HTTPS 保護主資料管理員 Web 應用程式  
  
1.  在確認 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式已經使用 HTTP 正確設定之後，在 IIS 中建立憑證。 如需詳細資訊，請參閱[在 IIS 7 中設定伺服器憑證](http://technet.microsoft.com/library/cc732230\(WS.10\).aspx)。  
  
2.  在 [連接] 窗格中，按一下 [網站] 底下主控 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式的網站。  
  
3.  在 [動作] 窗格中，按一下 [繫結]。  
  
4.  按一下 **[加入]**。  
  
5.  從清單中選取 [https]。  
  
6.  選取 SSL 憑證。  
  
7.  按一下 [確定] 。  
  
8.  選擇性。 若要移除 HTTP，讓使用者只能使用 HTTPS 存取網站，請從清單中按一下含有 **http** 的資料列。 按一下 [移除]，然後在確認對話方塊中按一下 [是]。  
  
    > [!IMPORTANT]  
    >  在移除 HTTP 之後，您必須變更 basicHttp 和 wsHttpBinding 組態。  
  
9. 若要關閉 [網站繫結] 對話方塊，請按一下 [關閉]。  
  
10. 現在開啟 *磁碟機*:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication 中的 web.config 檔案。  
  
11. 尋找字串 `<security mode="Message">` ，並將其變更為 `<security mode="Transport">`。  
  
12. 儲存並關閉檔案。 如果出現錯誤，這可能是因為您已啟用 UAC。 如需詳細資訊，請參閱 [關閉使用者帳戶控制](http://technet.microsoft.com/library/cc709691\(WS.10\).aspx)。 使用者現在應該能夠使用 HTTPS 存取網站。  
  
## <a name="see-also"></a>另請參閱  
 [建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
