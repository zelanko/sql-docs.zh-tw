---
title: 刪除和重新建立加密金鑰 (SSRS 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- re-creating encryption keys
- encryption keys [Reporting Services]
- deleting encryption keys
- symmetric keys [Reporting Services]
- removing encryption keys
- resetting encryption keys
ms.assetid: 201afe5f-acc9-4a37-b5ec-121dc7df2a61
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 38547a2d48ecbe1887702d7be9b45b3166d75243
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224813"
---
# <a name="delete-and-re-create-encryption-keys--ssrs-configuration-manager"></a>刪除和重新建立加密金鑰 (SSRS 組態管理員)
  刪除和重新建立加密金鑰是例行加密金鑰維護範圍之外的活動。 執行這些工作是為了因應報表伺服器所受的特定威脅，或者當您無法存取報表伺服器資料庫時的最後手段。  
  
-   您認為現有的對稱金鑰被洩漏時，請重新建立對稱金鑰。 也可以當成最佳安全性作法，定期重新建立金鑰。  
  
-   當您無法還原對稱金鑰時，請刪除現有的加密金鑰和無法使用的加密內容。  
  
## <a name="re-creating-encryption-keys"></a>重新建立加密金鑰  
 如果有證據顯示未授權使用者已獲悉對稱金鑰，或者您的報表伺服器已遭到攻擊，而您想要重設對稱金鑰做為預防，您就可以重新建立對稱金鑰。 重新建立對稱金鑰時，所有加密值都會使用新值重新加密。 如果您是在向外延展部署中執行多個報表伺服器，對稱金鑰的所有副本都會更新為新值。 報表伺服器使用它能使用的公開金鑰，來更新部署中每個伺服器的對稱金鑰。  
  
 唯有報表伺服器處於工作狀態時，您才能重新建立對稱金鑰。 重新建立加密金鑰和重新加密內容會中斷伺服器作業。 進行重新加密時，必須將伺服器離線。 重新加密過程中，不應該對報表伺服器提出任何要求。  
  
 您可以使用 Reporting Services 組態工具或 **rskeymgmt** 公用程式，來重設對稱金鑰和加密資料。 如需如何建立對稱金鑰的詳細資訊，請參閱[初始化報表伺服器 &#40;SSRS 設定管理員&#41;](ssrs-encryption-keys-initialize-a-report-server.md)。  
  
#### <a name="how-to-re-create-encryption-keys-reporting-services-configuration-tool"></a>如何重新建立加密金鑰 (Reporting Services 組態工具)  
  
1.  透過在 rsreportserver.config 檔案中修改 `IsWebServiceEnabled` 屬性，停用報表伺服器 Web 服務和 HTTP 存取。 此步驟會讓驗證要求暫時停止送給報表伺服器，而不會完全關閉伺服器。 您必須有最少的服務，好讓您可以重新建立金鑰。  
  
     如果您是重新建立報表伺服器向外延展部署的加密金鑰，請針對部署中的所有執行個體停用這個屬性。  
  
    1.  開啟 Windows 檔案總管並巡覽至 *drive*:\Program Files\Microsoft SQL Server\\<報表伺服器執行個體>\Reporting Services。 將 *drive* 取代成磁碟機代號並將 <報表伺服器執行個體> 取代成對應至您想要停用 Web 服務和 HTTP 存取之報表伺服器執行個體的資料夾名稱。 例如，C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services。  
  
    2.  開啟 rsreportserver.config 檔案。  
  
    3.  針對 `IsWebServiceEnabled` 屬性，指定 `False`，然後儲存您的變更。  
  
2.  啟動 Reporting Services 組態工具，然後連接到您要設定的報表伺服器執行個體。  
  
3.  在 [加密金鑰] 頁面上，按一下 **[變更]**。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  重新啟動報表伺服器 Windows 服務。 如果是重新建立向外延展部署的加密金鑰，請重新啟動所有執行個體上的服務。  
  
5.  透過在 rsreportserver.config 檔案中修改 `IsWebServiceEnabled` 屬性，重新啟用 Web 服務和 HTTP 存取。 如果是處理向外延展部署，請為所有執行個體執行此作業。  
  
#### <a name="how-to-re-create-encryption-keys-rskeymgmt"></a>如何重新建立加密金鑰 (rskeymgmt)  
  
1.  停用報表伺服器 Web 服務和 HTTP 存取。 使用前面程序中的指示來停止 Web 服務作業。  
  
2.  在主控報表伺服器的本機電腦上，執行 **[rskeymgmt.exe]** 。 使用 `-s` 引數來重設對稱金鑰。 不需要其他引數：  
  
    ```  
    rskeymgmt -s  
    ```  
  
3.  重新啟動 Windows 服務，並啟用 Web 服務作業。  
  
## <a name="deleting-unusable-encrypted-content"></a>刪除無法使用的加密內容  
 如果因故無法還原加密金鑰，報表伺服器將無法解密及使用以該金鑰加密的任何資料。 若要使報表伺服器回到工作狀態，必須刪除目前儲存在報表伺服器資料庫中的加密值，然後手動重新指定您需要的值。  
  
 刪除加密金鑰會從報表伺服器資料庫移除所有對稱金鑰資訊，並刪除任何加密內容。 所有未加密資料都不受影響；只會移除加密的內容。 刪除加密金鑰時，報表伺服器會加入新的對稱金鑰，自動將其本身重新初始化。 刪除加密內容時會發生下列情況：  
  
-   刪除共用資料來源中的連接字串。 執行報表的使用者會收到「尚未初始化 ConnectionString 屬性」錯誤。  
  
-   刪除預存認證。 報表與共用資料來源會重新設定成使用提示的認證。  
  
-   以模型為基礎的報表 (而且需要以預存認證或無認證設定共用資料來源) 將不會執行。  
  
-   停用訂閱。  
  
 一旦刪除加密內容，就無法再復原內容。 您必須重新指定連接字串和預存認證，也必須啟動訂閱。  
  
 您可以使用 Reporting Services 組態工具或 **rskeymgmt** 公用程式來移除值。  
  
#### <a name="how-to-delete-encryption-keys-reporting-services-configuration-tool"></a>如何刪除加密金鑰 (Reporting Services 組態工具)  
  
1.  啟動 Reporting Services 組態工具，然後連接到您要設定的報表伺服器執行個體。  
  
2.  按一下 **[加密金鑰]**，然後按一下 **[刪除]**。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  重新啟動報表伺服器 Windows 服務。 針對向外延展部署，為所有報表伺服器執行個體執行此作業。  
  
#### <a name="how-to-delete-encryption-keys-rskeymmgt"></a>如何刪除加密金鑰 (rskeymmgt)  
  
1.  在主控報表伺服器的本機電腦上，執行 **[rskeymgmt.exe]** 。 您必須使用 **-d** 套用引數。 下列範例說明您必須指定的引數：  
  
    ```  
    rskeymgmt -d  
    ```  
  
2.  重新啟動報表伺服器 Windows 服務。 針對向外延展部署，為所有報表伺服器執行個體執行此作業。  
  
#### <a name="how-to-re-specify-encrypted-values"></a>如何重新指定加密值  
  
1.  針對每個共用資料來源，您必須重新輸入連接字串。  
  
2.  針對使用預存認證的每個報表與共用資料來源，您必須重新輸入使用者名稱與密碼，然後儲存。 如需詳細資訊，請參閱《 [線上叢書》中的](../../integration-services/connection-manager/data-sources.md) 指定報表資料來源的認證和連接資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
3.  針對每個資料驅動訂閱，開啟每個訂閱，並重新輸入訂閱資料庫的認證。  
  
4.  針對使用加密資料的訂閱 (這包括使用加密的檔案共用傳遞延伸模組和協力廠商傳遞延伸模組)，開啟每個訂閱並重新輸入認證。 使用報表伺服器電子郵件傳遞的訂閱並不使用加密資料，因此不受金鑰變更的影響。  
  
## <a name="see-also"></a>另請參閱  
 [設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-manage-encryption-keys.md)   
 [儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
