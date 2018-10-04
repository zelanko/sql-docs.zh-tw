---
title: 將知識新增至知識庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
ms.assetid: da148a7f-55bc-4990-a157-e61968b831d7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f369ac83237e2e903515a168506e9b08ef396f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205540"
---
# <a name="adding-knowledge-to-a-knowledge-base"></a>將知識加入至知識庫
  此主題描述您可以在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中將知識加入至知識庫的方式。 在您可以執行資料品質作業之前，您必須擁有資料的相關知識。 您取得該項知識的方式是建立及維護資料品質知識庫，並將與特定類型之資料來源相關的知識加入至知識庫。 知識庫是有關資料的知識儲存機制，可讓您了解資料及維護資料的完整性。  
  
 知識庫包含與資料來源相關的資料定義域。 對於每一個資料定義域而言，DQKB 都會儲存所有識別的詞彙、拼字錯誤、驗證和商務規則，以及可用來針對資料來源執行資料品質動作的參考資料。 DQS 會使用這項知識來識別不正確或無效的資料，或是執行比對。  
  
 您可以透過以下電腦輔助或互動式方式，將知識加入至知識庫。  
  
-   [執行知識探索](#Discovery)  
  
-   [管理定義域中的資料值](#ManageDomain)  
  
-   [從 .dqs 檔案匯入知識](#DQSFile)  
  
-   [從 Excel 檔案匯入知識](#Excel)  
  
-   [將專案中的知識匯入回知識庫](#Project)  
  
-   [使用預設 DQS 知識庫](#Default)  
  
##  <a name="Discovery"></a> 執行知識探索  
 知識探索會針對資料品質準則分析資料取樣，然後將它取得的知識加入至知識庫。 這是電腦輔助的程序，可識別資料不一致和語法錯誤，並向資料建議變更。 知識探索活動是一個精靈，其中包括您可以互動方式在其上管理定義域值的頁面。  
  
-   如需詳細文件中的詳細資訊，請參閱[Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md)。  
  
-   如需示範如何執行知識探索的影片，請按一下 [這裡](http://msdn.microsoft.com/sqlserver/hh323825.aspx)。  
  
##  <a name="ManageDomain"></a> 管理定義域中的資料值  
 DQS 可讓您以互動方式變更及增加電腦輔助的知識探索活動所產生的中繼資料。 您會在 [定義域管理] 活動中執行這項作業，您可以在此活動中將變更套用至特定資料值。  
  
-   如需詳細文件中的詳細資訊，請參閱[Change Domain Values](../../2014/data-quality-services/change-domain-values.md)。  
  
-   如需示範如何執行定義域管理的影片，請按一下 [這裡](http://msdn.microsoft.com/sqlserver/hh323825.aspx)。 請注意，在此影片中，您會在知識探索精靈的 [管理定義域值] 頁面中變更定義域值。 您也可以在 [定義域管理] 活動的 [定義域值] 頁面中執行這些步驟。  
  
##  <a name="DQSFile"></a> 從 .dqs 檔案匯入知識  
 您可以將 .dqs 資料檔中的定義域匯入現有的知識庫，或者將 .dqs 中的整個知識庫匯入新的知識庫。 若要這樣做，您必須先將現有的定義域或知識庫匯出至 .dqs 檔案。 包含定義域的 .dqs 檔案會包含所有定義域資料；包含知識庫的 .dqs 檔案將包含所有知識庫資訊，包括定義域和比對原則。  
  
-   如需文件中的詳細資訊，請參閱[從 .dqs 檔案匯入定義域](../../2014/data-quality-services/import-a-domain-from-a-dqs-file.md)或[從 .dqs 檔案匯入知識庫](../../2014/data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)。  
  
##  <a name="Excel"></a> 從 Excel 檔案匯入知識  
 您可以將 Excel 試算表檔案中的定義域值匯入現有的定義域或知識庫。 若要這樣做，您必須先使用您想要匯入的定義域值建立 Excel 試算表，並確定 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 電腦上已安裝 Excel，好讓您能夠使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]匯入值。 您不能將定義域或知識庫中的定義域值匯出到 Excel 檔案。  
  
-   如需文件中的詳細資訊，請參閱[將 Excel 檔案中的值匯入至定義域](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md)或[在知識探索中匯入 Excel 檔案中的定義域](../../2014/data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)。  
  
##  <a name="Project"></a> 將專案中的知識匯入回知識庫  
 在您使用知識庫執行清理或比對資料品質專案之後，您可以將清理或比對期間建立的知識匯入回該知識庫。 這樣可讓您保存專案期間產生的知識，並持續在知識庫中建立知識。  
  
-   如需文件中的詳細資訊，請參閱[將清理專案值匯入定義域中](../../2014/data-quality-services/import-cleansing-project-values-into-a-domain.md)。  
  
##  <a name="Default"></a> 使用預設 DQS 知識庫  
 DQS 隨附在預先建立的知識庫 (稱為 DQS 資料) 中，其中包含美國公司和地址資料。 這個知識庫可用來快速啟動專案，不需要建立新的知識庫。 「DQS 資料」知識庫是唯讀的，但是資料監管可將它做為基礎建立新的知識庫。  
  
-   如需詳細文件中的詳細資訊，請參閱[使用 DQS 預設知識庫](../../2014/data-quality-services/using-the-dqs-default-knowledge-base.md)。  
  
  
