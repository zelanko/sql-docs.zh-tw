---
title: '[網站設定] 頁面（報表管理員） |Microsoft Docs'
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4d67a01c-eae4-49ba-a6e8-8e983c0248f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07fc0207020887d7e3ceb8716ee76c78a55d2bac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101115"
---
# <a name="site-settings-page-report-manager"></a>站台設定頁面 (報表管理員)
  您可以使用 [站台設定] 頁面來變更應用程式標題、針對報表記錄限制和報表處理逾時值設定整個網站的預設值、管理系統層級角色指派，以及管理共用排程。 您必須擁有「內容管理員」和「系統管理員」權限才能檢視此頁面。  
  
> [!NOTE]  
>  並非所有 SQL Server 版本都提供下列功能：報表記錄、報表執行和共用排程。 如需版本支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱[SQL Server 2014 版本支援的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-site-settings-page"></a>若要開啟站台設定頁面  
  
1.  開啟報表管理員。  
  
2.  在頁面的頂端，按一下 **[站台設定]**。 這樣就會開啟該站台的 [一般] 屬性頁面。  
  
     **注意：** 如果您在功能表中看不到 [**網站設定**] 選項，表示您沒有必要的許可權。如需詳細資訊，請參閱[設定原生模式報表伺服器以進行本機管理 &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)的「網站設定」一節。  
  
## <a name="options"></a>選項。  
 **名稱**  
 指定此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 報表管理員執行個體使用的標題。 根據預設，標題為 "[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]"。  
  
 **選取報表記錄的預設值**  
 選取要保留之報表記錄副本數目的預設值。 此預設值提供建立報表記錄限制的初始設定。 您可以在報表層級變更這些設定。 如需詳細資訊，請參閱[快照集選項屬性頁 &#40;報表管理員&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)。  
  
 如果稍後限制報表記錄，則當現有的報表記錄超過指定的限制時，報表伺服器會將現有的報表記錄縮減至低於新限制的量。 會先刪除最舊的報表快照集。 如果報表記錄為空白或在限制以下，則會加入新報表快照集。 如果達到限制，加入新報表快照集時會刪除最舊的快照集。  
  
 **報表執行逾時**  
 指定在特定秒數之後報表處理是否逾時。  
  
 此值會套用至報表伺服器上的報表處理。 它不會影響提供報表資料的資料庫伺服器上的資料處理。  
  
 報表處理計時器時鐘在選取報表時會開始，而當報表開啟時就會結束。 當您設定此值時，請指定足以完成資料處理和報表處理的時間。  
  
 **自訂報表產生器啟動 URL**  
 當報表伺服器不使用預設的報表產生器 URL 時，指定自訂 URL。 這個設定是選擇性的。 如果您沒有指定值，將會使用預設 URL，這樣會將報表產生器視為 ClickOnce 應用程式啟動。 預設的 URL 是下列其中一項：  
  
 **原生模式報表伺服器：** 在原生模式安裝中，預設 URL 會採用 HTTP://\<*computername*>/reportserver/reportbuilder/ReportBuilder_3_0_0_0. 應用程式的格式。  
  
 SharePoint 整合模式：預設 URL 的格式會是 HTTP://\<*SharePoint_site*>/_vti_bin/reportbuilder/ReportBuilder_3_0_0_0. 應用程式）。  
  
 **套用**  
 按一下即可儲存您對報表伺服器所做的變更。  
  
 **安全性**  
 按一下這個連結即可開啟 [系統角色指派] 頁面，在此頁面上您可以將使用者和群組帳戶指派至預先定義的系統角色。  
  
 **排程**  
 按一下此連結即可開啟 [排程] 頁面，在此頁面上您可以預先定義可供使用者為其報表和訂閱選取的共用排程。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [在原生模式報表伺服器上授與權限](security/granting-permissions-on-a-native-mode-report-server.md)   
 [預先定義的角色](security/role-definitions-predefined-roles.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
