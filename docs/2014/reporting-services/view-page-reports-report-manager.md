---
title: 檢視頁面上，報表 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4874ba29-429b-4dd4-a8cb-d4f087237dc2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d36a9e8b5e4b46283b78f07c27834a79993faeab
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59969435"
---
# <a name="view-page-reports-report-manager"></a>檢視頁面，報表 (報表管理員)
  使用報表的 [檢視] 頁面來檢視報表。 當您在「報表管理員」中第一次開啟報表時，它的格式為 HTML。 HTML 報表包含報表工具列，會顯示在報表的最上方，讓您能用來導覽報表頁面、在報表內進行搜尋，或是將報表匯出成不同的格式。 下列圖表顯示報表工具列。  
  
 ![報表工具列](media/htmlviewer-toolbar.gif "報表工具列")  
報表工具列  
  
 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中，您可以將報表設定為視需要執行，或是從報表執行快照集執行。 如果報表為視需要執行，則每次您開啟報表時都會進行所有的資料處理和報表處理。 如果您檢視的報表是設定為以報表執行快照集的方式執行，則是在建立快照集時進行資料處理。  
  
## <a name="exporting-reports"></a>匯出報表  
 並不是在所有的匯出格式中都可以使用所有的報表功能。 如果將 HTML 報表匯出成其他格式，則報表的顯示方式應該會有些差異。 此外，如果報表包含互動功能 (例如超連結、書籤或文件引導模式)，則在新的格式中可能無法使用這些功能，或者使用方式可能不同。  
  
## <a name="generating-data-feeds-from-report-data"></a>從報表資料產生資料摘要  
 您可以從報表產生資料摘要。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Atom 轉譯延伸模組會產生兩份符合 Atom 的文件：列出報表所提供之資料摘要的 Atom 服務文件，以及列出包含報表資料之資料摘要的 Atom 服務文件。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 會使用符合 Atom 1.0 的標準化格式來產生這些資料摘要，而且您可以使用取用符合 Atom 之資料摘要的應用程式來讀取與交換這些資料摘要。 例如， [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 用戶端可以取用從報表產生的資料摘要。  
  
## <a name="running-parameterized-reports"></a>執行參數化的報表  
 包含輸入欄位和 **[檢視報表]** 按鈕的報表，即為參數化報表。 若要檢視參數化報表，您可能需要提供用來執行報表的值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的所有版本都不能使用報表執行快照集和某些匯出格式。 如需詳細資訊，請參閱＜ [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
