---
title: DQS 中的 Reference Data Services | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 92112b0211536bcb964d71e538a92311b2579117
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027129"
---
# <a name="reference-data-services-in-dqs"></a>DQS 中的 Reference Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  參考資料指的是一組精確且完整的相關或已分類的全域資料 (在企業界限範圍之外)，這些資料是在可靠的公用網域或是由優質商業內容提供者所提供。  
  
 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的參考資料服務功能可讓您訂閱協力廠商參考資料提供者，並針對高品質資料來驗證您的商務資料，輕鬆地清理及豐富這些商務資料。 您可以使用 DQS 中主要 Data Quality Services 提供者的服務，在清除程序中標準化、更正或豐富您的資料。 例如，您可以針對參考資料使用區碼或郵遞區號的清單，以驗證客戶的地址。  
  
 參考資料服務功能具有以下優點：  
  
-   參考資料可讓您將資料與協力廠商擔保的資料做比較來確保資料的品質。  
  
-   參考資料程序會併入 DQS 知識庫建立和資料品質專案中，好讓您建立全面性的資料品質程序。  
  
-   支援使用 Windows Azure Marketplace 所提供的參考資料，以及直接從協力廠商參考資料提供者所提供的參考資料。  
  
##  <a name="Marketplace"></a> 使用 Windows Azure Marketplace 所提供的參考資料  
 DQS 支援使用 Windows Azure Marketplace 所提供的參考資料，好讓內容提供者透過服務商場提供參考資料服務。 服務商場是 Microsoft 的服務，可針對高品質資料和應用程式提供單一服務商場和傳遞通道，並提供雲端服務。 如需市集的詳細資訊，請參閱[深入了解 Windows Azure Marketplace ](https://go.microsoft.com/fwlink/?LinkId=211291) (https://go.microsoft.com/fwlink/?LinkId=211291)。  
  
 服務商場與 DQS 之間的順暢整合會簡化與探索、瀏覽及取得 DQS 內的資料品質專案資訊相關的步驟。 這些資料是從 DQS 取用，而且有助於 DQS 使用者以創新方式將 DQS、服務商場和參考資料服務提供者結合在一起，以達成高資料品質。  
  
 若要針對清理活動在 DQS 中使用服務商場的參考資料，您必須擁有服務商場帳號金鑰。 建立服務商場帳號金鑰是免費的，只有當您訂閱付費的資料集時才需要付費。 訂閱及使用免費的資料集不需要支付任何費用。 如需有關建立市集帳戶金鑰的詳細資訊，請參閱[建立您的帳戶](https://go.microsoft.com/fwlink/?LinkId=212936) (https://go.microsoft.com/fwlink/?LinkId=212936)。  
  
 此外，您可以從 DQS 執行下列服務商場活動：  
  
-   瀏覽服務商場中的資料集。  
  
-   建立服務商場帳號金鑰。  
  
-   管理您的服務商場帳戶詳細資料，例如帳號金鑰及資料提供者訂閱。  
  
 在 **中，您可以在** [組態] **畫面的** [參考資料] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]索引標籤上執行這些活動。  
  
##  <a name="Direct"></a> 使用直接從協力廠商參考資料提供者所提供的參考資料  
 如果您未連接到網際網路而無法使用服務商場，DQS 也支援您的組織網路中所提供之資料提供者的直接連接。 若要使用直接線上協力廠商參考資料提供者所提供的參考資料，您必須為 DQS 中的資料提供者建立記錄。  
  
##  <a name="HowToCleanse"></a> 如何使用參考資料清理資料  
 使用參考資料在 DQS 中清理資料包括以下三個步驟：  
  
1.  **在 DQS 中設定參考資料提供者詳細資料**：您必須先在 DQS 中設定參考資料服務詳細資料，才能在 DQS 中使用參考資料。  
  
    1.  如果您使用服務商場，請提供有效的服務商場帳號金鑰、瀏覽至服務商場中的 [Data Quality Services](https://go.microsoft.com/fwlink/?LinkId=227587) 資料類別目錄，並訂閱所需的提供者。  
  
    2.  如果您使用直接線上參考資料提供者，您必須先在 DQS 中加入直接參考資料提供者詳細資料，然後才可以使用它。  
  
     在 DQS 中設定參考資料提供者詳細資料對於特定資料提供者而言是一次性的活動。 只有 DQS 管理員可以在 DQS 中設定參考資料設定。  
  
2.  **將知識庫中的定義域/複合定義域對應至參考資料服務**：將定義域/複合定義域對應至步驟 1 所訂閱/新增的適當參考資料服務。  
  
3.  **在資料品質專案中將對應的定義域用於清理活動**：在針對 [清理] 活動建立資料品質專案時，請選取包含定義域/複合定義域的知識庫 (這些定義域與步驟 2 中的參考資料服務相對應)，並執行清理活動。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何設定 DQS 使用服務商場或直接線上協力廠商資料提供者所提供的參考資料服務。|[設定 DQS 使用參考資料](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|描述如何將知識庫中的定義域/複合定義域對應至參考資料服務。|[將網域或複合網域附加至參考資料](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|描述如何使用參考資料服務清理資料。|[使用參考資料 &#40;外部&#41; 知識清理資料](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
  
