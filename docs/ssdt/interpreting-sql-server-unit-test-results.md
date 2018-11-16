---
title: 解譯 SQL Server 單元測試結果 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: fde3c95b-2f68-483d-a197-0f7161b72fa3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0576454d646f5e738e153f7937cb717f8b26fc3
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51658937"
---
# <a name="interpreting-sql-server-unit-test-results"></a>解譯 SQL Server 單元測試結果
當您執行 SQL Server 單元測試時，會自動產生測試結果、將其儲存到磁碟，並於 [測試結果] 視窗中摘要列出。 啟動測試回合之後，[測試結果] 視窗隨即出現並顯示測試回合的進度。 這個顯示畫面包括執行中的測試以及已完成的測試。  
  
若要查看與測試結果有關的詳細資訊，請在 [測試結果] 視窗中按兩下該測試結果，即可顯示 [測試結果詳細資料] 頁面。 如需測試結果的詳細資訊，請按兩下測試結果。  
  
如需如何變更 [測試結果] 視窗顯示內容的詳細資訊，請參閱[如何：在測試視窗中加入或移除資料行 (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182508(VS.100).aspx) 或[如何：在測試視窗中加入或移除資料行 (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182508.aspx)。  
  
## <a name="storing-test-results"></a>儲存測試結果  
單元測試的結果會自動儲存在硬碟的檔案中，而這些檔案的副檔名為 .trx。 .trx 檔案是一種包含測試回合詳細資料的 XML 檔案。 您可以從之前的測試回合載入 .trx 檔案，以便檢閱這些測試回合的結果或是重新執行之前的測試。 如需詳細資訊，請參閱[如何：重新執行測試 (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182472(VS.100).aspx)。  
  
> [!NOTE]  
> 您不可以從遠端執行單元測試。  
  
如果您的小組使用 Visual Studio Team Foundation Server Team 專案協助管理其工作，您也可以將測試資料發行至 SQL Server 資料庫 (又稱為「作業存放區」)。  
  
如需如何儲存測試結果、重複使用測試結果以及將測試結果與小組分享的詳細資訊，請參閱[如何：在 Visual Studio 2010 中儲存和開啟測試結果](https://msdn.microsoft.com/library/ms404662(VS.100).aspx)或[如何：在 Visual Studio 2012 中儲存和開啟測試結果](https://msdn.microsoft.com/library/ms404662.aspx)。  
  
## <a name="see-also"></a>另請參閱  
[執行 SQL Server 單元測試](../ssdt/running-sql-server-unit-tests.md)  
  
