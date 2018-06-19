---
title: 資料分析工作和檢視器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], about data profiling
- data profiling
- profiling data
ms.assetid: 756840e3-aa09-45cd-9951-1a17af4b5925
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b1c1d793495a5d7d779cbbec008289ba0aa09a1d
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35400840"
---
# <a name="data-profiling-task-and-viewer"></a>資料分析工作和檢視器
  「資料分析」工作提供擷取、轉換和載入資料之處理內部的資料分析功能。 您可以使用「資料分析」工作來獲得下列好處：  
  
-   更有效率地分析來源資料  
  
-   深入了解來源資料  
  
-   在資料品質問題引進資料倉儲前加以預防。  
  
> [!IMPORTANT]  
>  資料分析工作僅用於儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的資料。 此工作不適用於協力廠商或以檔案為基礎的資料來源。  
  
## <a name="data-profiling-overview"></a>資料分析概觀  
 資料品質對於每個企業都相當重要。 企業會在其交易系統頂層建立分析和商業智慧系統，因此，關鍵效能指標和資料採礦預測的可靠性完全取決於它們所依據之資料的有效性。 雖然商務決策之有效資料的重要性與日遽增，但是確定此資料之有效性的挑戰也日漸重要。 資料會不斷從各種系統和來源以及大量使用者串流到企業。  
  
 資料品質的標準專屬於網域或應用程式，因此可能難以定義。 定義資料品質的一個常見方式為資料分析。  
  
 資料分析是有關資料之彙總統計資料的集合，可能包括：  
  
-   Customer 資料表中的資料列數。  
  
-   [州] 資料行中的相異值數目。  
  
-   [郵遞區號] 資料行中的 null 或遺漏值的數目。  
  
-   [城市] 資料行中之值的散發。  
  
-   [郵遞區號] 資料行上，[州] 資料行之功能相依性的強度，也就是說，對於給定的郵遞區號值而言，州永遠相同。  
  
 資料設定檔所提供的統計資料可提供您所需的資訊，以便將使用來源資料時可能發生的品質問題有效地降到最低。  
  
## <a name="integration-services-and-data-profiling"></a>Integration Services 與資料分析  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，資料分析程序由下列步驟所組成：  
  
 **步驟 1：設定資料分析工作**  
 「資料分析」工作是一種工作，可用於設定您要計算的設定檔。 然後，您可以執行包含「資料分析」工作的封裝以計算設定檔。 此工作會將設定檔輸出以 XML 格式儲存到檔案或封裝變數。  
  
 **如需詳細資訊，請參閱**[資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。  
  
 **步驟 2：檢閱資料分析工作計算的設定檔**  
 若要檢視「資料分析」工作計算的資料設定檔，您可以將輸出傳送到檔案，然後使用「資料設定檔檢視器」即可。 這個檢視器是一個獨立的公用程式，可以用摘要和詳細資料格式，顯示具有選擇性向下鑽研能力的設定檔輸出。  
  
 **如需詳細資訊，請參閱**[資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
### <a name="addition-of-conditional-logic-to-the-data-profiling-workflow"></a>將條件式邏輯加入資料分析工作流程  
 「資料分析」工作沒有內建的功能，您無法根據設定檔輸出，使用條件式邏輯將此工作連接到下游工作。 不過，您可以利用少量的程式設計，在「指令碼」工作中輕鬆加入這個邏輯。 例如，「指令碼」工作可以根據「資料分析」工作的輸出檔，執行 XPath 查詢。 此查詢可以判斷特定資料行中，null 值的百分比是否超出特定的臨界值。 如果百分比超出臨界值，您可以中斷封裝，並解決來源資料中的問題，然後再繼續。 如需詳細資訊，請參閱 [在封裝工作流程中納入資料分析工作](../../integration-services/control-flow/incorporate-a-data-profiling-task-in-package-workflow.md)。  
  
## <a name="related-content"></a>相關內容  
 [資料分析工具結構描述](http://go.microsoft.com/fwlink/?LinkId=251524)  
  
  
