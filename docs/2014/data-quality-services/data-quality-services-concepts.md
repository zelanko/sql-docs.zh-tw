---
title: Data Quality Services 概念 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 837c71ee-48fa-4044-8744-2be9119aaa04
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 649d687b93a2eeff940c92c79b7b966511a1d79d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792946"
---
# <a name="data-quality-services-concepts"></a>Data Quality Services 概念
  本主題將提供知識管理、資料品質專案和資料品質管理中 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 概念的簡短摘要。  
  
##  <a name="Knowledge"></a> 知識管理概念  
 DQS 知識庫是資料管理人或 IT 專業人員所建立的中繼資料儲存機制，可用於透過資料清理和資料比對改善資料品質。 DQS 知識管理包括以電腦輔助方式和互動方式建立並管理知識庫所使用的處理序。  
  
 **知識探索**  
  
 知識探索是一種電腦輔助的處理序，它會分析組織資料的樣本，以便建置資料的相關知識。 一旦您擁有分析的結果之後，就可以驗證並強化知識，然後進行套用，以便執行資料清理、比對和分析。 如需詳細資訊，請參閱 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
 **定義域管理**  
  
 定義域管理處理序可讓您變更或增加知識探索處理序所產生的知識。 您可以用互動方式編輯、更新和檢閱知識庫中的知識。 知識庫是由資料定義域組成，這些定義域包含定義域值及其狀態、定義域規則、以詞彙為主的關聯，以及參考資料。 在定義域管理中，您可以變更定義域屬性、將參考資料附加至定義域、管理定義域規則、管理定義域值並輸入資料關聯，以及建立、刪除、匯入或匯出定義域。 您也可以使用彙總多個定義域的複合定義域。 如需詳細資訊，請參閱 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
 **比對原則**  
  
 比對原則會包含用來執行刪除重複資料作業的比對規則。 比對原則處理序可讓您建立比對規則、根據比對結果和分析資料進行微調，以及將原則加入至知識庫。 如需詳細資訊，請參閱 [資料比對](../../2014/data-quality-services/data-matching.md)。  
  
 **Reference Data Services**  
  
 您可以使用參考資料來驗證、更正和充實資料，並運用保證其參考資料品質之公司的服務。 您可以使用 Windows Azure Marketplace 的服務來連接到參考資料提供者，也可以使用提供者的直接連接。 如需詳細資訊，請參閱 [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md)。  
  
 如需有關 DQS 中知識管理的詳細資訊，請參閱＜ [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
##  <a name="Projects"></a> 資料品質專案概念  
 資料管理人會在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式中使用資料品質專案來執行資料品質作業 (清理和比對)。  
  
 **資料清理**  
  
 DQS 中的資料清理是根據 DQS 知識庫中的知識來完成。 DQS 中的資料清理是兩個步驟的程序：  
  
-   **電腦輔助的清理**：DQS 會使用所選知識庫中用於清理專案的知識，針對資料來源中的值提出更正/建議。  
  
-   **互動式清理**：資料負責人可以執行互動式清理程序，以便變更或增加電腦輔助資料清理程序已經建議的資料更正。 資料管理人會使用資料清理處理序所識別的信賴等級和統計資料，或在專案中手動輸入自己的變更，藉以完成此作業。  
  
 清理資料之後，資料管理人可以將已處理的資料匯出至 SQL Server 資料庫、.csv 或 Excel 檔案。 如需詳細資訊，請參閱 [Data Cleansing](../../2014/data-quality-services/data-cleansing.md)。  
  
 **資料比對**  
  
 比對處理序可讓資料管理人比較資料，以便透過刪除重複處理序校正相似但稍微不同的資料。 DQS 會根據知識庫中包含的比對規則執行刪除重複作業。資料管理人會在資料品質專案內部指定比對處理序的參數。 如需詳細資訊，請參閱 [Data Matching](../../2014/data-quality-services/data-matching.md)。  
  
 **分析與通知**  
  
 執行資料品質專案時，資料分析會為資料管理人提供有關 DQS 正在針對清理或比對活動處理之資料的即時統計資料和資訊。 資料分析可協助您評估資料品質專案中之清理和比對活動的效用，而通知可協助使用者採取動作以強化資料清理和資料比對活動。 如需詳細資訊，請參閱 [Data Profiling and Notifications in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md)。  
  
 如需有關 DQS 中資料品質專案的詳細資訊，請參閱[資料品質專案 &#40;DQS&#41;](../../2014/data-quality-services/data-quality-projects-dqs.md)。  
  
##  <a name="Admin"></a> 資料品質管理概念  
 DQS 系統管理員可以使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式來執行各種管理工作。  
  
 **活動監控**  
  
 活動監控會顯示在某個資料範圍內執行之每項活動的狀態、提供每項活動的資料，並且讓 DQS 系統管理員控制活動。 如需詳細資訊，請參閱 [Monitor DQS Activities](../../2014/data-quality-services/monitor-dqs-activities.md)。  
  
 **Configuration**  
  
 [組態] 選項可讓您：  
  
-   設定參考資料服務設定。 如需詳細資訊，請參閱 [Configure DQS to Use Reference Data](../../2014/data-quality-services/configure-dqs-to-use-reference-data.md)。  
  
-   設定清理與比對活動的臨界值。 如需詳細資訊，請參閱 [設定清理和比對的臨界值](../../2014/data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)。  
  
-   啟用/停用分析通知。 如需詳細資訊，請參閱[啟用或停用 DQS 中的分析通知](../../2014/data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)。  
  
-   在活動層級或更進階的模組層級設定 DQS 記錄檔的嚴重性層級。 如需詳細資訊，請參閱 [Configure Severity Levels for DQS Log Files](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md)。  
  
 **DQS 安全性**  
  
 您可以使用 SQL Server 安全性機制中的角色來確保 DQS 安全。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式具有三個決定使用者存取層級的 DQS 角色：dqs_administrator、dqs_kb_editor 和 dqs_kb_operator。 您無法使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式，將角色授與使用者。這項作業是使用 SQL Server Management Studio 來完成的。 如需詳細資訊，請參閱 [DQS Security](../../2014/data-quality-services/dqs-security.md)。  
  
 如需有關 DQS 管理的詳細資訊，請參閱＜ [DQS Administration](../../2014/data-quality-services/dqs-administration.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [Data Quality Services](../../2014/data-quality-services/data-quality-services.md)  
  
  
