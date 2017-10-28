---
title: "在報表伺服器項目的 Windows SharePoint Services 中使用內建安全性 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 9577e88d-c22b-4934-936f-e0f1400cedf5
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: becc8fac740023906166f8a9545139300c233a51
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="use-built-in-security-in-windows-sharepoint-services-for-report-server-items"></a>在 Windows SharePoint Services 中使用報表伺服器項目的內建安全性
  SharePoint 提供內建安全性功能，可用來存取 SharePoint 網站和文件庫中的報表伺服器項目。 如果您已經指定網站和清單權限給使用者，則在設定 SharePoint 和報表伺服器之間的整合設定之後，那些相同的使用者就能立即存取報表伺服器項目和作業。  
  
## <a name="securable-items"></a>安全性實體項目  
 您可以使用在網站或文件庫上定義的權限來授與報表伺服器項目的存取權。 不過，如果您要保護個別項目的安全，可以設定下列內容類型的權限：  
  
|檔案類型|說明|  
|---------------|-----------------|  
|.rdl|報表定義檔案，定義報表配置和用來擷取資料的命令。 報表定義會在處理報表時，使用資料來源連接資訊擷取資料。 如果報表定義是先前在報表產生器中建立的特定報表，則報表會與在轉譯報表中，設定資料瀏覽範圍的報表模型 (.smdl) 檔案配對。|  
|.smdl|報表模型檔案，描述資料結構與彼此相關聯的方式， 可用來建立和執行報表產生器報表。|  
|.rsds|共用資料來源檔案，指定外部資料來源的連接資訊。 此檔案是由報表定義 (.rdl) 和報表模型 (.smdl) 檔案使用。 報表模型固定使用 .rsds 檔取得基礎資料來源的連接資訊。 報表定義可以使用 .rsds 檔，或是使用在報表上的資料來源屬性中定義的連接資訊。|  
|.rsc|報表組件檔案，可定義報表項目或資料區的配置和結構。 它用來將報表組件發行至伺服器，讓其他報表作者可以重複使用報表組件庫中的項目。|  
|.rsd|共用資料集檔案，可定義資料集的查詢語法和屬性。 您可以從報表外部共用、儲存、處理與快取共用資料集。|  
  
 排程、訂閱和報表記錄都不是安全性實體項目。 您可以在網站或程式庫上設定權限，決定使用者是否可以建立或使用排程、訂閱和報表記錄，但無法直接保護這些項目的安全。  
  
 若要保護個別項目的安全，請在文件庫中選取該項目，按一下向下箭號，然後選取 **[管理權限]**。 在 **[動作]** 功能表上，選取 **[編輯權限]**。  
  
## <a name="using-built-in-groups-and-permission-levels-to-access-report-server-items"></a>使用內建群組和權限等級存取報表伺服器項目  
 當您使用權限繼承和標準 SharePoint 群組時，可以在設定報表伺服器和 SharePoint 執行個體上的整合設定之後，立即存取大部分的報表伺服器作業。  
  
 SharePoint 所提供的標準群組會對應預先定義的權限等級，以決定在 SharePoint 網站上存取文件和頁面的方式。 如果您使用標準群組和預設權限等級，而站台設定為繼承權限，則可以利用下列方式使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能：  
  
|**SharePoint 群組**|**權限等級**|**摘要**|**報表伺服器存取權**|  
|---------------------------|--------------------------|-----------------|------------------------------|  
|**擁有者**|完整控制|擁有者具有完整權限，可以建立、管理和保護報表伺服器項目和作業。|設定權限，以控制整個網站上程式庫中儲存的所有報表伺服器項目的存取權。 設定報表模型內的權限 (亦稱為模型項目安全性)。 自訂報表檢視器 Web 組件。 將報表和其他項目加入程式庫。 編輯報表和其他文件的項目屬性。 刪除報表和其他項目。 檢視報表，包括使用報表模型進行資料瀏覽的報表。 設定報表上的參數。 設定報表上的處理選項。 產生報表模型。 在報表產生器中建立報表。 建立和管理共用資料來源。 建立、變更和刪除任何使用者所擁有的訂閱。 建立和管理整個網站使用的共用排程。 建立和管理文件的版本，包括報表記錄。 下載報表定義或報表模型的來源檔案。 取代報表定義、報表模型、共用資料來源或資源 (保留項目屬性和權限)。|  
|**成員**|參與|成員可以建立新的項目，並從設計工具將項目報表和模型發行至 SharePoint 程式庫。|將報表和其他項目加入程式庫。 編輯報表和其他文件的項目屬性。 刪除報表和其他項目。 檢視報表，包括使用報表模型進行資料瀏覽的報表。 檢視過去的文件，包括報表記錄快照集 (使用者還必須具備權限以開啟所建立報表記錄的報表)。 設定報表上的參數。 設定報表上的處理選項。 產生報表模型。 在報表產生器中建立報表。 建立和管理共用資料來源。 建立、變更和刪除使用者所擁有的訂閱。 搭配訂閱使用共用排程。 建立和管理文件的版本，包括報表記錄。 下載報表定義或報表模型的來源檔案。 取代報表定義、報表模型、共用資料來源或資源 (保留項目屬性和權限)。|  
|**訪客** 和 **檢視者**|讀取|訪客可以檢視報表|檢視報表，包括使用報表模型進行資料瀏覽的報表。|  
  
 如果您不是使用內建群組和權限等級，則必須加入特定權限，才能存取 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能。 如需詳細資訊，請參閱 [在 SharePoint Web 應用程式中設定報表伺服器作業的權限](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [授與權限在 SharePoint 網站上的報表伺服器項目](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services to SharePoint Groups and Permissions 中比較角色和工作](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [在 SharePoint Web 應用程式中設定報表伺服器作業的權限](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [授與權限在 SharePoint 網站上的報表伺服器項目](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  

