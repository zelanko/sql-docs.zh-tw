---
title: 在報表伺服器上偵測到自訂延伸模組（Upgrade Advisor） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- rendering extensions [Reporting Services], custom extensions
- security extensions [Reporting Services]
- custom extensions [Reporting Services]
- data processing extensions [Reporting Services], custom extensions
- delivery extensions [Reporting Services]
ms.assetid: fa184bd7-11d6-4ea3-9249-bc1b13db49e5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2149e0434c13ccc9e284385999cf94c98fb937fa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059381"
---
# <a name="custom-extensions-were-detected-on-the-report-server-upgrade-advisor"></a>在報表伺服器上偵測到自訂延伸模組 (Upgrade Advisor)
  Upgrade Advisor 偵測到組態檔中有自訂延伸模組設定，表示您的安裝包括用於資料處理、傳遞、轉譯、安全性或驗證的一個或多個自訂延伸模組。 升級作業將會一起移動延伸模組的組態設定與升級的報表伺服器。 不過，如果自訂延伸模組安裝在現有的報表伺服器安裝資料夾中，這些自訂延伸模組的組件檔將不會在升級程序期間移至新的安裝資料夾。 升級完成之後，您必須將這些組件檔移至新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝資料夾。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]提供可擴充的架構，可讓開發人員建立資料處理、傳遞、轉譯、安全性和驗證的自訂延伸模組。  
  
 如果自訂延伸模組或組件使用於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝中，雖然您可以使用安裝程式來執行升級，但是可能必須在升級完成之後將延伸模組移至新的安裝位置，或者可能必須在升級之前執行一些步驟。  
  
> [!NOTE]  
>  Upgrade Advisor 不會偵測出自訂程式碼組件是否設定成在報表中用於計算項目值、樣式和格式。 如需詳細資訊，請參閱[其他 Reporting Services 升級問題](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)。  
  
 如果您從軟體廠商購買了自訂延伸模組，請詢問廠商是否有關於升級自訂功能的其他資訊。  
  
## <a name="corrective-action"></a>更正動作  
 您可以使用下列各節來判斷執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的升級之外或之前要執行的步驟：  
  
 [自訂資料處理或傳遞延伸模組](#dataprocdeliver)  
  
 [自訂轉譯延伸模組](#render)  
  
 [SQL Server 2000 報表伺服器上的自訂安全性或驗證延伸模組](#secauth2000)  
  
 [SQL Server 2005 報表伺服器上的自訂安全性或驗證延伸模組](#secauth2005)  
  
 升級完成之後，請將這些延伸模組組件移至新的安裝資料夾，然後確認自訂延伸模組是否如預期方式運作。 如果您的延伸模組無法運作，可能必須重新編譯它。  
  
#### <a name="to-recompile-an-extension"></a>重新編譯延伸模組  
  
1.  將 Microsoft.ReportingServices.Interfaces.dll 檔複製到包含原始程式碼的資料夾。  
  
2.  開啟包含來源檔案的專案，然後加入 Microsoft.ReportingServices.Interfaces.dll 檔的參考。  
  
3.  重建方案，以便繫結此延伸模組。  
  
 如果您決定不要繼續進行升級，可能會決定改為移轉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 如需遷移自訂擴充功能的步驟，請參閱本主題中的[遷移自訂擴充](#migrcustext)功能。  
  
###  <a name="custom-data-processing-or-delivery-extensions"></a><a name="dataprocdeliver"></a>自訂資料處理或傳遞延伸模組  
 如果 Upgrade Advisor 偵測到自訂資料處理或傳遞延伸模組，系統並不會封鎖升級程序。 不過，升級完成之後，您可能必須先執行其他步驟，然後這些延伸模組所提供的自訂功能才能正常運作。 例如，如果自訂延伸模組檔案安裝在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝資料夾中，您就必須執行其他步驟。  
  
##### <a name="post-upgrade-steps-for-custom-data-processing-or-delivery-extensions"></a>自訂資料處理或傳遞延伸模組的升級後步驟  
  
1.  將延伸模組檔案移至報表伺服器的新程式資料夾。 根據預設，報表伺服器程式資料夾位於 \Program Files\Microsoft SQL Server \ MSRS10_50。 \<*instance_name*>\report sample 伺服器。  
  
 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜部署資料處理延伸模組＞和＜實作傳遞延伸模組＞。  
  
###  <a name="custom-rendering-extensions"></a><a name="render"></a>自訂轉譯延伸模組  
 如果 Upgrade Advisor 偵測到自訂轉譯延伸模組，系統就會封鎖升級程序。 您可以從組態檔中移除自訂延伸模組的組態項目，藉以繼續進行升級程序。 不過，這樣做將會導致升級完成之後，使用者無法使用自訂延伸模組。 如果您在升級之後需要自訂轉譯延伸模組，就必須建立更新的轉譯延伸模組，或是向自訂延伸模組供應商取得更新的轉譯延伸模組。  
  
 您必須執行一些步驟來啟用升級，或者您可能會選擇改為移轉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
> [!IMPORTANT]  
>  在您已經測試並確認更新的轉譯延伸模組如預期方式運作之前，請勿升級或移轉報表伺服器。  
  
##### <a name="to-upgrade-custom-rendering-extensions"></a>升級自訂轉譯延伸模組  
  
1.  取得含有最新介面的轉譯延伸模組。  
  
2.  從 RSReportServer.config 中移除舊的自訂轉譯延伸模組項目。  
  
3.  升級報表伺服器。  
  
4.  升級完成之後，請在報表伺服器上安裝更新的延伸模組。  
  
 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜實作轉譯延伸模組＞。  
  
###  <a name="custom-security-or-authentication-extensions-on-a-sql-server-2000-report-server"></a><a name="secauth2000"></a>SQL Server 2000 報表伺服器上的自訂安全性或驗證延伸模組  
 如果 Upgrade Advisor 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 報表伺服器上偵測到自訂安全性或驗證延伸模組，系統就會封鎖升級程序。 您必須執行一些步驟來啟用升級，或者您可能會選擇改為移轉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 不論是哪一種情況，您都必須使用 Microsoft.ReportingServices.Interfaces.dll 中的最新介面來更新和重新編譯延伸模組，因為這些介面已經在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 與 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之間變更。  
  
> [!IMPORTANT]  
>  在您已經測試並確認更新的安全性或驗證延伸模組如預期方式運作之前，請勿升級或移轉報表伺服器。  
  
 如果您要使用針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 所建立的自訂驗證延伸模組，就必須修改原始程式碼，以便支援針對模型驅動報表所導入的新類別和成員。  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2000-report-server"></a>若要從 SQL Server 2000 報表伺服器升級自訂安全性或驗證延伸模組  
  
1.  使用最新的介面來更新並重新編譯任何安全性或驗證延伸模組。  
  
2.  從 RSReportServer.config 中移除安全性或驗證延伸模組項目。  
  
3.  升級報表伺服器。  
  
4.  升級完成之後，請在報表伺服器上安裝更新的延伸模組。  
  
 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜實作安全性延伸模組＞。  
  
###  <a name="custom-security-or-authentication-extensions-on-a-sql-server-2005-report-server"></a><a name="secauth2005"></a>SQL Server 2005 報表伺服器上的自訂安全性或驗證延伸模組  
 如果 Upgrade Advisor 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 報表伺服器上偵測到自訂安全性或驗證延伸模組，系統就會封鎖升級程序。 您必須執行一些步驟來啟用升級，或者您可能會選擇改為移轉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2005-report-server"></a>升級來自 SQL Server 2005 報表伺服器的自訂安全性或驗證延伸模組  
  
1.  從 RSReportServer.config 中移除安全性或驗證延伸模組的組態項目。  
  
2.  升級報表伺服器。  
  
3.  升級完成之後，請將這些組態項目重新加入 RSReportServer.config 中。  
  
4.  如果延伸模組組件安裝在舊的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝資料夾中，請將它們移至新的安裝資料夾。  
  
 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜實作安全性延伸模組＞。  
  
###  <a name="migrating-custom-extensions"></a><a name="migrcustext"></a>遷移自訂擴充功能  
 如果您決定要移轉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 而非執行升級，請使用下列步驟，將自訂延伸模組移轉至新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體。  
  
##### <a name="to-migrate-custom-extensions-to-a-new-reporting-services-instance"></a>將自訂延伸模組移轉至新的 Reporting Services 執行個體  
  
1.  建立或取得含有最新 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 介面的更新延伸模組。  
  
2.  將報表伺服器移轉至新的執行個體。  
  
3.  在新的執行個體上設定延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Upgrade Advisor Reporting Services 升級問題&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
