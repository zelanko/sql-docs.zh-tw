---
title: 使用資料摘要的庫 (PowerPivot for SharePoint) 共用資料摘要 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data feeds [Analysis Services with SharePoint]
ms.assetid: 4ec98dec-0cd2-4727-bb79-5bf6f8a865d6
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ac02a4f06eb66528d68ba42b3036d0837f308d4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161389"
---
# <a name="share-data-feeds-using-a-data-feed-library-powerpivot-for-sharepoint"></a>使用資料摘要庫共用資料摘要 (PowerPivot for SharePoint)
  資料摘要是從以 Atom 電傳格式公開資料之服務或應用程式產生的 XML 資料流， 現在越來越常用在應用程式之間傳輸資料，以及傳輸資料至用戶端檢視器。 在 PowerPivot for SharePoint 部署中，資料摘要用來填入[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]具有以 Atom 感知應用程式或服務的資料來源。  
  
 如果您已經使用 Atom 感知應用程式的組合，您可能永遠都不需要知道摘要是如何產生和取用的，因為應用程式之間會進行完美的資料傳輸。 但是，使用自訂方案來發行 Atom 摘要的組織通常都需要想辦法提供摘要給資訊工作者使用。 其中一種辦法就是：建立並共用資料服務文件 (.atomsvc) 檔，以提供連接到產生摘要的線上來源。 資料摘要庫是有特殊用途的程式庫，支援在 SharePoint Web 應用程式中建立並共用資料服務文件。  
  
 本主題包含下列幾節：  
  
 [必要條件](#prereq)  
  
 [建立資料服務文件](#createdsdoc)  
  
 [保護資料服務文件的安全](#securedsdoc)  
  
 [修改資料服務文件](#modifydsdoc)  
  
 [下一步：使用資料服務文件](#usedsdoc)  
  
> [!NOTE]  
>  雖然資料摘要是用來將 Web 資料加入您在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中建立的 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]資料來源，但是任何可讀取 Atom 摘要的用戶端應用程式都可以處理資料服務文件。  
  
##  <a name="prereq"></a> 必要條件  
 您必須已部署[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]PowerPivot for SharePoint，以便將[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]查詢處理，SharePoint 伺服器陣列。 資料摘要支援是透過 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 方案套件進行部署。  
  
 您必須有支援資料服務文件內容類型的 SharePoint 文件庫。 因此，建議您使用預設的資料摘要庫，但是您也可以手動方式加入該內容類型至任何文件庫。 如需詳細資訊，請參閱 <<c0> [ 建立或自訂資料摘要庫&#40;PowerPivot for SharePoint&#41;](create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md)。</c0>  
  
 您必須有資料服務或線上資料來源，提供 Atom 1.0 格式的 XML 表格式資料。  
  
 您必須在 SharePoint 網站上擁有「參與」權限，以便在 SharePoint 文件庫中建立或管理資料服務文件。  
  
##  <a name="createdsdoc"></a> 建立資料服務文件  
 所謂資料服務文件是持續性的串流資料要求，在以摘要格式提供資料的線上資料來源或應用程式要求之後開始進行。 當您建立資料服務文件時，是指定指標，指向一個或多個 URL 可定址資料服務，這些服務會以 Atom 新聞訂閱方式格式提供 XML 表格。  
  
 單一文件可以指定多份資料摘要。 如果您想要在單一匯入作業中，從相同的服務 (或甚至不同的服務) 擷取一組資料裝載，這項功能會很有用。  
  
1.  在 SharePoint 網站上，開啟資料摘要庫，或已經加入並設定資料服務內容類型的另一個文件庫。 若要尋找先前已建立的資料摘要庫，請按一下 [快速啟動] 上的 [全部檢視]。  
  
2.  在頁面頂端功能區上的 [文件工具] 中，按一下 [文件]。  
  
3.  按一下 [新增文件]，然後選取 [資料服務文件]。  
  
4.  在 [新資料服務文件] 頁面中輸入下列資訊：  
  
    1.  資料服務文件的名稱和描述。 請務必提供充分的詳細資料，讓使用者可以判斷是否使用該摘要。  
  
    2.  在資料摘要中，輸入以 Atom 1.0 格式提供資料之資料服務或 Web 應用程式的 URL。  
  
         URL 必須解析成傳回以資料列和資料行組成之結構化或半結構化資料的服務。 服務應該以匿名方式，或透過目前使用者的安全性認證，傳回資料。  
  
         URL 必須解析成支援 Windows 驗證、基本驗證或匿名存取的服務。 匯入摘要的使用者可指定所要使用的配置。 系統會預設為選取整合式安全性。  
  
         資料摘要 URL 可以包含參數。 不同類型的資料服務技術支援進階 URL 定址配置，可讓您精確地選取所要使用的資料。 例如，ADO.NET Data Services 提供 URL 參數，以供指定基礎資料中的實體、關聯和瀏覽路徑。 藉由指定複雜的 URL 做為資料摘要的來源，您可以精確地指定所要使用的資料集。  
  
    3.  針對相同的資料摘要，輸入資料表名稱，以便後續用來識別用戶端應用程式中的資料集。 在 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]中，您匯入的每份資料摘要都放在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來源內摘要本身的資料表控制項中。 當您設定資料摘要時，必須指定接收匯入資料的資料表名稱。  
  
5.  按一下「加入其他資料摘要」，以重複先前的步驟，指定相同服務或不同服務的其他摘要。  
  
     每份資料服務文件都做為單一作業處理。 文件中所有資料摘要都會以非同步方式產生，並傳回至相同作業中的用戶端應用程式。 因此，只能指定您要一起使用之資料摘要的 URL 資料表對。  
  
     由於驗證配置是在資料服務文件層級設定，所以每一份額外資料摘要的來源服務或應用程式都必須支援與第一份摘要相同的驗證配置。 在相同資料服務文件之中的所有摘要，都會在執行階段以相同方法進行驗證。  
  
6.  儲存文件。 資料服務文件是以實體檔案 (.atomsvc) 儲存於內容庫中，內容庫必須已設定為此內容類型。  
  
 若要使用資料服務文件，您可以在 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 中開啟 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿，然後在 [匯入資料精靈] 中選擇 [從資料摘要] 選項。 接到提示時，使用者要指定資料服務文件的 SharePoint URL，以啟動資料匯入作業。 如需詳細資訊，請參閱 <<c0> [ 使用資料摘要&#40;PowerPivot for SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md)。</c0>  
  
##  <a name="securedsdoc"></a> 保護資料服務文件的安全  
 資料服務文件會繼承包含該文件之文件庫的權限。 您在項目上設定的權限會決定使用者是否可以開啟、修改或刪除資料服務文件。  
  
 若要使用資料服務文件做為資料摘要匯入 PowerPivot 用戶端應用程式中，使用者只需要在文件上擁有檢視權限。 檢視權限就已足夠，可在 [匯入精靈] 中解析 URL。  
  
 資料服務文件的檢視權限只有在資料摘要匯入作業開始時，才會進行檢查。 匯入之後，文件上的權限不會持續不斷地進行檢查，已加入至 PowerPivot 資料來源的摘要則成為靜態資料，而與提供原始連接資訊的資料服務文件中斷連接。  
  
 同樣地，您後續排程的任何資料重新整理作業也會排除資料服務文件。 在匯入時，每份摘要的連接資訊都會複製到 PowerPivot 資料來源中，以便進行重新整理。 因此，進行資料重新整理時並不會檢查資料服務文件上的權限，因為在重新整理作業中永遠不會參考該文件本身。  
  
|工作|SharePoint 權限需求|  
|----------|----------------------------------------|  
|匯入資料摘要至啟用 PowerPivot 功能的活頁簿。|文件庫中的資料服務文件的檢視權限。|  
|在 PowerPivot 用戶端應用程式中，重新整理先前透過摘要擷取的資料。|不適用。 PowerPivot 用戶端應用程式會使用內嵌 HTTP 連接資訊，直接連接到提供摘要的資料服務和應用程式。 PowerPivot 用戶端應用程式不會使用資料服務文件。|  
|在 SharePoint 伺服器陣列中，重新整理資料以排程工作方式執行，並不需要使用者輸入。|不適用。 PowerPivot 服務會使用內嵌 HTTP 連接資訊，以直接連接至提供摘要的資料服務和應用程式。 PowerPivot 服務不會使用資料服務文件。|  
|刪除文件庫中的資料服務文件|文件庫的「參與」權限。|  
  
##  <a name="modifydsdoc"></a> 修改資料服務文件  
 您可以新增、編輯或移除資料服務文件中的個別 URL 資料表項目。 儲存您所做的變更之後，在新匯入作業中選取服務文件的使用者將取得您指定的資料摘要。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 使用舊版文件的活頁簿不會受到您所做任何變更的影響。 這是因為資料服務文件只在初始匯入作業期間讀取一次。 在匯入期間，服務 URL 和資料表名稱會進行複製，並儲存在活頁簿內部。 之後，就可以使用這些內部值來執行後續的重新整理作業，以取得更新後的資料。  
  
 由於 SharePoint 網站上的資料服務文件與含匯入摘要的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿之間並沒有持續的連結，因此修改資料服務文件的任何部分並不會對現有的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿造成任何影響。  
  
> [!IMPORTANT]  
>  雖然資料服務文件只讀取一次，但提供實際資料的資料服務可以定期進行存取，以取得更新的摘要。 如需如何重新整理資料的詳細資訊，請參閱[PowerPivot 資料重新整理](power-pivot-data-refresh.md)。  
  
##  <a name="usedsdoc"></a> 下一步：使用資料服務文件  
 若要使用您在 SharePoint 文件庫中建立資料服務文件，您使用**從資料摘要**匯入 PowerPivot 資料來源中的選項。 如需相關指示，請參閱 <<c0> [ 使用資料摘要&#40;PowerPivot for SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot 資料摘要](power-pivot-data-feeds.md)  
  
  
