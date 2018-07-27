---
title: 第 5 課： 自動化清理和比對使用 SSIS |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
caps.latest.revision: 8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 91d0310663c738f524101f0bb4862c2db2d89cf3
ms.sourcegitcommit: d457bb828eb46ee83f8ff5bdecfff09b26d7b154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/26/2018
ms.locfileid: "39259783"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>第 5 課：使用 SSIS 自動化清理和比對
  在第 1 課方法，您可以建置供應商知識庫，並使用它來清理資料，在第 2 課和比對資料使用工具第 3 課**DQS 用戶端**。 在真實世界案例中，您可能要從來源 DQS 不支援，或者您想要自動化清理和比對程序中提取資料，而不需要使用**DQS 用戶端**工具。 SQL Server Integration Services (SSIS) 有可供您整合各種異質來源的資料的元件和 **[DQS 清理轉換](http://msdn.microsoft.com/library/ee677619.aspx)** 叫用清理元件DQS 所公開的功能。 目前，DQS 不會公開比對功能給 SSIS 使用，但您可以使用**[模糊群組轉換](http://msdn.microsoft.com/library/ms141764.aspx)** 來識別資料中的重複項。  
  
 您可以使用資料上傳至 MDS**實體式暫存功能**。 當您在 MDS 中建立實體時，將會自動建立對應的暫存資料表和預存程序。 例如，當您建立 Supplier 實體時， **stg.supplier_Leaf**資料表並**stg.udp_Supplier_Leaf**自動建立預存程序。 您會使用暫存資料表和程序來建立、更新及刪除實體成員。 在這一課，您會建立 Supplier 實體的新實體成員。 為了將資料載入 MDS 伺服器，SSIS 封裝會先將資料載入暫存資料表 stg.supplier_Leaf，然後觸發相關的預存程序 stg.udp_Supplier_Leaf。 請參閱[匯入資料](http://msdn.microsoft.com/library/ee633726.aspx)如需詳細資訊。  
  
 在這一課，您會執行下列工作：  
  
1.  在 MDS 中移除供應商資料 (如果您已經完成之前的四個課程)。 您在這一課建立的 SSIS 封裝會將資料自動上傳至 MDS。 您在稍早已使用 DQS 用戶端，手動將已清理和比對的供應商資料上傳至 MDS 伺服器。  
  
2.  請在 Supplier 實體中建立訂閱檢視，向其他應用程式公開此實體中的資料。 此動作會建立一個 SQL 檢視表，您將使用 SQL Server Management Studio 加以驗證。 您不會在這一版的教學課程中使用這個檢視表。  
  
3.  建立及執行 SSIS 專案使用**SQL Server Data Tools**。 專案會使用**資料清理**轉換，以將清理要求提交到 DQS 伺服器。 DQS 尚未公開比對功能，因此您會使用**模糊群組**轉換來識別重複項目。  
  
4.  確認已使用主資料管理員在 MDS 中建立資料。  
  
5.  檢閱 SSIS 封裝所建立之 DQS 清理專案的結果，並選擇性地執行互動式清理，進一步建立知識庫。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 1&#40;必要條件&#41;： 在 MDS 中移除供應商資料](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
