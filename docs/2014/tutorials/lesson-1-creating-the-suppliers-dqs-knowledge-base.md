---
title: 第 1 課：建立供應商 DQS 知識庫 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 78825ccb-30fc-463c-8140-435532e2ecd2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 7aa0e4755de7f358596c7ce477367d84646fd176
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62676037"
---
# <a name="lesson-1-creating-the-suppliers-dqs-knowledge-base"></a>第 1 課：建立供應商 DQS 知識庫
  在這一課，您會建立名為 DQS 知識庫**供應商**有關供應商資料的知識 （中繼資料）。 您會使用知識庫，針對輸入供應商資料執行清理和比對活動。 清理活動會識別不正確/無效資料、更正不正確的資料、提出更正/建議、標準化資料，並以更多資訊來充實資料。 比對活動會比較資料及識別資料中類似的記錄 (但有些不同)，以幫助您移除資料的重複項。  
  
 您可以使用互動式和電腦輔助程序來建立、建置及管理知識庫。 知識庫中的知識是在定義域中維護，其中每個定義域都專屬於資料中您想要清理及/或比對的某個資料欄位。  
  
 在這一課，您可以執行下列工作來建立**供應商**知識庫：  
  
-   建立名為 DQS 知識庫**供應商**。 您可以使用幾個方式建立知識庫。 您可以從頭建立知識庫，或是根據現有的知識庫來建立知識庫，方法是匯入包含預建及匯出之知識庫的 DQS 檔案 (.dqs) 或針對取樣資料執行知識探索活動。 在本教學課程中，您會從頭建立知識庫。  
  
-   建立中的網域**供應商**知識庫用於清理資料和比對資料來識別重複項。 建立的定義域是針對您想要用於清理和比對活動的資料欄位，而不是用於資料中的所有資料欄位。  
  
-   將值加入定義域的方式是手動加入值、從 Excel 檔案匯入值、針對取樣資料執行知識探索活動，以及從清理專案匯入專案值。 您也可以匯入包含定義域屬性和值的 DQS 檔案來匯入定義域值，您不會在本教學課程執行這個方式。  
  
-   為定義域設定規則。 定義域規則是 DQS 用來驗證、更正並標準化定義域值的條件。  
  
-   為定義域設定以詞彙為主的關聯。 以詞彙為主的關聯可讓您針對屬於定義域值的詞彙進行更正。 例如，在值**Contoso Inc.，Inc.** 是可以定義為 Incorporated 的詞彙。 如此有助於標準化資料以及識別重複項。 例如， **Contoso Inc.** 並**Contoso Incorporated**可以視為重複項目。  
  
-   在定義域值中指定同義字。 您可以設定兩個或多個值當做同義字，並設定其中一個值當做前置值，這個值在清理活動期間會取代它的同義字值，以標準化資料。  
  
-   建立名為「地址驗證」的複合定義域，其中包含 Address line、City、State 和 Zip 等定義域。 複合定義域是由一個或多個單一定義域所組成的定義域。 它可讓您建立牽涉到多個定義域的規則。 例如，您可以定義規則：如果 City 為 Los Angeles，State 必須是 CA，其中 City 和 State 是不同的定義域。  
  
-   設定及使用參考資料服務。 Data Quality Services (DQS) 中的參考資料服務功能可讓您訂閱協力廠商參考資料提供者，並針對高品質資料來驗證您的商務資料，以清理及豐富這些商務資料。 您可以使用 DQS 中主要 DQS 提供者的服務，在清除程序中標準化、更正或豐富您的資料。 在本教學課程中，您將學習如何設定 DQS 環境在 Windows Azure Marketplace 使用參考資料服務，並使用與「地址驗證」複合定義域相關的服務來清理地址資料。  
  
-   發行知識庫，好讓知識庫可用於清理和比對活動。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 1:建立知識庫和定義域](../../2014/tutorials/task-1-creating-a-knowledge-base-and-domains.md)  
  
  
