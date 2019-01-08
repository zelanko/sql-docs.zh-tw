---
title: 使用從 RDL 結構描述 （SSRS 教學課程） 產生的類別更新報表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RDL [Reporting Services], generating
- RDL [Reporting Services], tutorials
- RDL [Reporting Services], serializing
ms.assetid: 8f81d48f-7ab9-4ef8-bce0-7d16d9a47fbd
author: craigg-msft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2f104892e3ee8a8c542c41bc07789a94ab8d0c4e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53349379"
---
# <a name="updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial"></a>使用 RDL 結構描述產生的類別更新報表 (SSRS 教學課程)
  本教學課程說明如何使用 XML 結構描述定義工具 (Xsd.exe) 來產生類別，可讓您序列化和還原序列化報表定義檔案 （.rdl 和.rdlc） 搭配[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] <xref:System.Xml.Serialization.XmlSerializer>類別。  
  
## <a name="what-you-will-learn"></a>學習內容  
 這個教學課程進行期間，您將完成下列活動：  
  
-   建立應用程式使用[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)]主控台應用程式專案範本。  
  
-   從使用您建立報表定義語言 (RDL) 結構描述產生類別**xsd**工具。  
  
-   連接到報表伺服器，並擷取報表定義。  
  
-   撰寫程式碼，以更新報表定義檔案。  
  
-   將已更新的報表定義存回報表伺服器。  
  
-   執行 RDL 結構描述應用程式 (VB/C#)。  
  
> [!NOTE]  
>  如果報表沒有描述，本教學課程提供的程式碼範例可能會失敗。 發生失敗是因為報表未指定描述以致描述屬性不存在。  
  
## <a name="requirements"></a>需求  
 若要完成教學課程，必須具備下列項目：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]。  
  
-   足以存取及發行報表至報表伺服器所在電腦之報表伺服器 Web 服務的權限。  
  
-   安裝到 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 執行個體的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 範例資料庫。  
  
-   安裝在您報表伺服器中的報表。 本教學課程使用範例報表 Company Sales 2012。 如需有關範例報表的詳細資訊，請參閱 < [SQL Server Reporting Services 產品範例](https://go.microsoft.com/fwlink/?LinkId=177889)。  
  
> [!NOTE]  
>  安裝期間不會自動安裝範例，但是您可在任何時間加以安裝。 有關範例的詳細資訊，請參閱[SQL Server Product Samples](https://go.microsoft.com/fwlink/?LinkId=182887)。  
  
 **若要完成本教學課程的估計的時間：** 30 分鐘  
  
## <a name="tasks"></a>工作  
 [第 1 課：建立 RDL 結構描述 Visual Studio 專案](../../2014/tutorials/lesson-1-create-the-rdl-schema-visual-studio-project.md)  
  
 [第 2 課：使用 xsd 工具的 RDL 結構描述產生類別](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md)  
  
 [第 3 課：從報表伺服器載入報表定義](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)  
  
 [第 4 課：以程式設計方式更新報表定義](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)  
  
 [第 5 課：將報表定義發行到報表伺服器](../../2014/tutorials/lesson-5-publish-the-report-definition-to-the-report-server.md)  
  
 [第 6 課：執行 RDL 結構描述應用程式&#40;VB C&#35;&#41;](../../2014/tutorials/lesson-6-run-the-rdl-schema-application-vb-csharp.md)  
  
## <a name="see-also"></a>另請參閱  
 [報表定義語言 &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
