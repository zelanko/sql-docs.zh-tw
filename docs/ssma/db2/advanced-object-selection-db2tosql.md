---
title: " (DB2ToSQL) 的 Advanced 物件選取專案 |Microsoft Docs"
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ca098c15-c343-4d7d-a284-c2fc405eb991
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f59e442a70b8c9b621f453ab9837412238ec6102
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937257"
---
# <a name="advanced-object-selection-db2tosql"></a> (DB2ToSQL) 的 Advanced 物件選取範圍
[**高級物件區段**] 對話方塊可讓您使用物件名稱中的字串和子字串來篩選資料庫物件，然後選取或取消選取那些物件。 SSMA 會對選取的物件執行轉換和遷移作業。  
  
若要存取此對話方塊，請以滑鼠右鍵按一下 [中繼資料瀏覽器]，然後選取 [**先進物件選取專案**]。  
  
當您第一次開啟對話方塊時，請按一下 [**顯示子類別目錄專案**]，以顯示所有已將中繼資料載入專案中的物件。 然後，您可以輸入字串來篩選項目。 例如，輸入字串 "company" 以顯示名稱包含該字串的所有專案。  
  
使用此對話方塊之前，您可能會想要強制 SSMA 藉由轉換架構或儲存專案來載入所有中繼資料。  
  
## <a name="options"></a>選項。
**檢查所有專案**  
在 [所有專案] 旁邊加入核取記號。 這些專案會立即在 [中繼資料瀏覽器] 中選取。  
  
**取消核取所有專案**  
移除 [所有專案] 旁的核取記號。 這些專案會立即在 [中繼資料瀏覽器] 中清除。  
  
**清單視圖模式**  
在清單中顯示篩選的專案。  
  
**資料表視圖模式**  
在資料表中顯示篩選的專案。  
  
**僅顯示已載入的專案**  
切換類別或專案的顯示。 選取此按鈕時，[SSMA] 會顯示符合篩選準則的所有專案，以及先前載入的專案。 未選取此按鈕時，SSMA 會顯示類別目錄資料夾。  
  
**Filter**  
輸入您要用來篩選項目的字串。 例如，若要尋找專案名稱中包含字串 "ID" 的所有可用專案，請在 [**篩選**] 方塊中輸入字串 "id"。  
  
如果專案符合篩選準則，則會在您輸入字串時顯示類別或專案。 若要查看相符的專案，建議您按一下 [**只顯示已載入的專案**] 按鈕。  
  
**清除篩選**  
清除**篩選**方塊。  
  
