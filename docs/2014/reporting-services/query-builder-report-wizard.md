---
title: 查詢產生器（報表精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.dataview.vdtquerydesigner.f1
- sql12.rtp.rptwizard.querybuilder.f1
helpviewer_keywords:
- Query Builder [Reporting Services]
ms.assetid: 1b0904ea-28c1-448e-b56c-c0fdfbc8b222
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8d289466fcff56a78172c54f24a093e0af169484
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108000"
---
# <a name="query-builder-report-wizard"></a>查詢產生器 (報表精靈)
  使用查詢產生器，即可指定查詢以擷取使用於報表中的結果集。 您可以在兩種查詢產生器之間進行選擇：  
  
-   以文字為基礎的查詢產生器 (預設) 會提供簡單的工作空間，讓您指定查詢和檢視結果。 您可以指定多個 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式、自訂資料處理延伸模組的查詢或命令語法，以及指定為運算式的查詢。 因為一般查詢產生器不會前置處理查詢，而且可以容納各種查詢語法，所以它是報表設計師的預設查詢產生器工具。  
  
-   圖形化查詢產生器可以提供較豐富的視覺體驗。 它會用於 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的其他部分中。 如果您並未建立運算式或多重部分 SQL 陳述式，則可以使用圖形化查詢產生器。  
  
     若要切換至圖形化查詢產生器，請切換視窗左上角的 **[當成文字編輯]** 按鈕。  
  
 您也可以從其他報表匯入查詢。  
  
## <a name="query-builder-options"></a>查詢產生器選項  
 **當做文字編輯**  
 在以文字為基礎和圖形化查詢設計工具之間切換 (如果這兩種工具都適用於查詢的話)。  
  
 **匯入**  
 開啟 [匯入查詢]**** 對話方塊，然後顯示任何可用報表的 .rdl 和 .sql 檔。 您可以依原狀使用匯入的查詢，也可以在查詢產生器中修改此查詢。  
  
 **!進行**  
 執行查詢，如果查詢有效則傳回結果集。 請注意，如果這是一個運算式，則無法執行查詢。 若要驗證以運算式為基礎的查詢，您必須預覽報表。  
  
 **命令類型**  
 指定文字、預存程序或直接指定資料表。 命令類型的可用性會視您指定的資料處理延伸模組而定。  
  
 **查詢窗格**  
 輸入查詢。  
  
 **結果窗格**  
 顯示查詢傳回的結果集。  
  
## <a name="see-also"></a>另請參閱  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [報表精靈說明](../../2014/reporting-services/report-wizard-help.md)  
  
  
