---
title: Master Data Services 概觀 (MDS) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- 何謂主要資料
helpviewer_keywords:
- Master Data Services, overview
- Master Data Services
ms.assetid: 8a4c28b1-6061-4850-80b6-132438b8c156
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 66cee237e12729f494aa1ed0e915db145ff5d076
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62448117"
---
# <a name="master-data-services-overview-mds"></a>Master Data Services 概觀 (MDS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題說明 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]的索引鍵資料組織和管理功能。 
  
 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 可讓您管理組織的一組主要資料。 您可以將資料組織到模型、建立用來更新資料的規則，並控制誰更新資料。 使用 Excel，您可以在組織中與其他人共用主要資料集。 
  
 >  如需 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 架構的說明，請參閱 simple-talk.com 上的 [Master Data Services - 基本概念](https://www.simple-talk.com/sql/database-delivery/master-data-services-basics) 文件。 如需 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中新功能的資訊，請參閱 [Master Data Services 的新功能 &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)  
   **如需如何安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]、設定資料庫和網站，以及部署範例模型的指示，請參閱** [Master Data Services 安裝和組態](../master-data-services/master-data-services-installation-and-configuration.md)。  
  
 在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，此模型是您主要資料結構中的最上層容器。 您可以建立模型來管理各種類似資料分類，例如管理線上產品資料組。 模型包含一或多個實體，而實體又包含成員，亦即資料記錄。 實體類似於資料表。  
  
 例如，您的線上產品模型可能包含產品、色彩及樣式等實體。 色彩實體可能包含紅色、銀色及黑色等色彩成員。  
  
 ![色彩實體](../master-data-services/media/mds-productmodel-colorentity-composite.png "色彩實體")  
  
 模型也包含實體中所定義的屬性。 屬性包含可以協助說明實體成員的值， 包括沒有特定格式的屬性與網域屬性。  網域屬性包含由實體成員填入的值，可用為其他實體的屬性值。  
  
 例如產品實體在費用與權數上可能會有沒有特定格式的屬性。 而且會有色彩 ![數字 1](../master-data-services/media/mds-number1.png "數字 1") 的網域屬性，其中包含由色彩實體成員所植入的值。 此主要色彩清單用作「產品」實體的屬性值![數字 2](../master-data-services/media/mds-number2.png "數字 2")。  
  
 ![色彩的網域屬性](../master-data-services/media/mds-productentity-color-domainattribute.png "色彩的網域屬性")  
  
 衍生的階層由模型中實體之間的關聯性而來。 這些是網域屬性關聯性。 例如，在產品模型中，您可以有色彩衍生階層![數字 1](../master-data-services/media/mds-number1.png "數字 1")，其來自色彩![數字 2](../master-data-services/media/mds-number2.png "數字 2") 與產品![數字 3](../master-data-services/media/mds-number3.png "數字 3") 實體之間的關聯性。  
  
 ![色彩衍生階層](../master-data-services/media/mds-derivedhierarchy.png "色彩衍生階層")  
  
 當您為資料定義基本結構之後，就可開始使用匯入功能加入資料記錄 (成員)。 您將資料載入暫存資料表、使用商務規則驗證資料，以及將資料載入 MDS 資料表。  您也可以使用商務規則來設定屬性值。  
  
 下表摘要列出 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 的主要工作。 除非另有指示，否則您必須是模型系統管理員，才能完成下列所有程序。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
> [!NOTE]  
>  安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]後，您可能想要在測試環境中完成下列工作，並使用所提供的範例資料。 如需詳細資訊，請參閱[部署模型 &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)。  
  
|動作|詳細資料|相關主題|  
|------------|-------------|--------------------|  
|建立模型|模型建立時會被視為 VERSION_1。|[模型 &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)<br /><br /> [建立模型 &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)|  
|建立實體|視需要建立多個實體以包含成員。|[實體 &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)<br /><br /> [建立實體 &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)|  
|建立實體當做網域屬性|若要建立網域屬性，請先建立實體來擴展屬性值清單。|[網域屬性 &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)<br /><br /> [建立網域屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|建立實體的屬性|建立屬性以描述成員。 Name 和 Code 屬性會自動包含在每個實體，且無法移除。 您可能想要建立其他自由格式屬性來包含文字、日期、數字或檔案。|[屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)<br /><br /> [建立文字屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)<br /><br /> [建立數值屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-numeric-attribute-master-data-services.md)<br /><br /> [建立日期屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-date-attribute-master-data-services.md)<br /><br /> [建立連結屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-link-attribute-master-data-services.md)<br /><br /> [建立檔案屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)|  
|建立屬性群組|如果實體有四個或五個以上的屬性，您可能想要建立屬性群組。  這些群組是在 [總管] 中方格上方顯示的索引標籤，透過在個別索引標籤上群組屬性，方便導覽。|[屬性群組 &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)<br /><br /> [建立屬性群組 &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|匯入支援實體的成員|使用暫存處理序匯入支援實體的資料。 針對 Product 模型，這表示匯入色彩或大小。 您也可以手動建立成員。<br /><br /> <br /><br /> 注意:如果使用者至少擁有實體分葉模型物件的 [更新] 權限且可存取 [總管] 功能區域，他們就可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中建立成員。|[概觀：從資料表匯入資料 &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)<br /><br /> [建立分葉成員 &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|建立並套用商務規則以確保資料品質|建立及發行商務規則，確保資料的正確性。 您可以使用商務規則：<br /><br /> 設定預設屬性值。<br /><br /> 變更屬性值。<br /><br /> 在資料未通過商務規則驗證時，傳送電子郵件通知。|[商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)<br /><br /> [建立及發行商務規則 &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)<br /><br /> [根據商務規則驗證特定成員 (Master Data Services)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)<br /><br /> [設定電子郵件通知 &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)<br /><br /> [設定商務規則來傳送通知 &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|匯入主要實體的成員以及套用商務規則|使用暫存處理序，匯入主要實體的成員。 完成後，驗證版本，將商務規則套用到模型版本中的所有成員。<br /><br /> 然後您可以更正任何商務規則驗證問題。|[驗證 &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)<br /><br /> [根據商務規則驗證版本 &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)<br /><br /> [驗證預存程序 &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)|  
|建立衍生階層|衍生的層級可隨您的商務需求改變而更新，以確保所有成員皆位於適當的層級中。|[衍生階層 &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)<br /><br /> [建立衍生階層 &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|如有需要，建立明確階層|如果您想要建立的階層不是以層級為基礎且包含單一實體的成員，可以建立明確階層。|[明確階層 &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)<br /><br /> [建立明確階層 &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|如有需要，建立集合|如果您想要檢視成員的不同群組進行報告或分析，而且不需要完整的階層，請建立集合。<br /><br /> <br /><br /> 注意:如果使用者至少擁有集合模型物件的 [更新] 權限且可存取 [總管] 功能區域，他們就可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中建立集合。|[集合 &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)<br /><br /> [建立集合 &#40;Master Data Services&#41;](../master-data-services/create-a-collection-master-data-services.md)|  
|建立使用者定義的中繼資料|若要描述模型物件，請將使用者定義的中繼資料加入至模型。 中繼資料可能包含物件擁有者或資料來源。||  
|鎖定模型版本以及指派版本旗標|鎖定模型版本，以防止系統管理員以外的使用者變更成員。 在版本的資料成功通過商務規則驗證之後，您就可以認可版本，防止所有使用者變更成員。<br /><br /> 建立版本旗標，並將它指派至模型。 旗標可幫助使用者和訂閱系統來識別所要使用之模型的版本。|[版本 &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)<br /><br /> [鎖定版本 &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)<br /><br /> [建立版本旗標 &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)|  
|建立訂閱檢視|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 若要讓訂閱系統取用主要資料，請建立訂閱檢視，在  資料庫中建立標準檢視。|[概觀：匯出資料 &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)<br /><br /> [建立訂閱檢視以匯出資料 &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|設定使用者和群組的權限|您無法將使用者和群組的權限從測試環境複製到實際執行環境。 但可以使用測試環境來判斷最終要用於實際執行的安全性。|[安全性 &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)<br /><br /> [新增群組 &#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)<br /><br /> [新增使用者 &#40;Master Data Services&#41;](../master-data-services/add-a-user-master-data-services.md)|  
  
 準備就緒時，您可以將包含或不含資料的模型部署至實際執行環境。 如需詳細資訊，請參閱[部署模型 &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)。  
  
  

