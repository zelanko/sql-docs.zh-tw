---
title: 大量載入安全性考量 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, XML Bulk Load
- bulk load [SQLXML], security
- security [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], security
ms.assetid: 192fc6d4-ecbc-4a4d-a5cb-55e1f64af318
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a3c304302f17c360dd9bb3a0ac51c7ea50bce40d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777600"
---
# <a name="bulk-load-security-considerations-sqlxml-40"></a>大量載入安全性考量 (SQLXML 4.0)
  下面是使用 XML 大量載入的安全性指導方針：  
  
-   當您指定要將大量載入作業當做交易執行時，可以使用 `TempFilePath` 屬性來指定要在其中建立暫存檔的資料夾。  
  
     大量載入處理序會使用下列權限來建立這些暫存檔：  
  
    -   讀取/寫入/刪除存取權會授與大量載入處理序。  
  
    -   讀取權限會授與所有使用者，因為 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用來存取這些檔案的帳戶是未知的。 您可以針對包含這些暫存檔的資料夾設定適當的權限，藉以限制它們的存取權。  
  
-   XML 大量載入本身沒有任何權限設定。 系統會假設資料庫已正確設定，而且使用者內容 (亦即，設定要使用大量載入的登入) 已設定適當的權限。  
  
-   在非交易式模式中，如果大量載入處理序期間發生錯誤，資料可能會維持部分載入的狀態。 大量載入只會在發生錯誤的時間點停止。 交易式模式可用來減少這個問題。  
  
-   發生大量載入錯誤時，它們可能會包含資料庫的相關資訊。 例如，它們可能會包含資料表或資料行的名稱，或資料行類型資訊。 當您使用大量載入時，就應該謹慎地捕捉來自大量載入處理序的錯誤並且傳回一般錯誤訊息，而非直接將錯誤公開給使用者。  
  
-   大量載入不會對它所處理的資料量設定任何限制。 大量載入不會針對要載入的資料大小進行任何檢查。 執行大量載入的使用者必須負責確保系統有足夠的記憶體可處理指定的檔案，而且資料庫有足夠的空間可儲存所載入的資料。  
  
-   大量載入不會嘗試使用以程式碼方式提供的資料。 系統絕對不會以任何方式執行資料輸入。 輸入資料中的任何程式碼或命令會都被視為一般資料，不會加以執行。  
  
-   大量載入可能會根據 XML 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料模型之間的差異，對給定資料進行格式上的變更。 例如，指定時間的格式是不同的。 大量載入會嘗試解決這些差異。 結果是某些精確度的資訊可能會遺失。  
  
-   大量載入不會對其用來處理資料的時間量設定限制。 在處理完成或發生錯誤之前，都會繼續進行處理。  
  
-   大量載入可以在資料庫內部建立和刪除暫存資料表，而且需要權限才能這樣做。 這些資料表的權限將提供給連接至資料庫的相同使用者，以便進行大量載入處理序。  
  
-   大量載入可以建立和刪除在交易式模式處理期間使用的暫存檔，而且需要權限才能這樣做。 建立這些檔案所使用的權限與執行大量載入之執行緒的目前使用者相同。  
  
-   如果使用者設定了讓 SQLXML 寫入錯誤的錯誤記錄檔，每次執行大量載入時，系統都會使用上一個大量載入處理序的資料來覆寫該檔案。  
  
## <a name="see-also"></a>另請參閱  
 [執行大量載入 XML 資料的&#40;SQLXML 4.0&#41;](../bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
  
  
