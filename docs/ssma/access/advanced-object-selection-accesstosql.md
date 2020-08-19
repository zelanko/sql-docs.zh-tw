---
description: AccessToSQL) 的 Advanced Object Selection (
title: AccessToSQL) 的 Advanced Object Selection (|Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4d2b367f-8ac7-4534-b66f-10300ef64ebc
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0b5dfe862f48b2669d0535066fe36e4a892c5dfa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418584"
---
# <a name="advanced-object-selection--accesstosql"></a>AccessToSQL) 的 Advanced Object Selection (
[ **Advanced Object 區段** ] 對話方塊可讓您使用物件名稱中的字串和子字串來篩選資料庫物件，然後選取或取消選取這些物件。 SSMA 會在選取的物件上執行轉換和遷移作業。  
  
若要存取這個對話方塊，請以滑鼠右鍵按一下 [中繼資料瀏覽器]，然後選取 [ **Advanced Object Selection**]。  
  
當您第一次開啟對話方塊時，按一下 [ **顯示子類別專案** ]，即可顯示所有已載入至專案之中繼資料的物件。 然後，您可以輸入字串來篩選項目。 例如，輸入字串 "company" 來顯示所有名稱包含該字串的專案。  
  
使用這個對話方塊之前，您可能會想要強制 SSMA 藉由轉換架構或儲存專案來載入所有中繼資料。  
  
## <a name="options"></a>選項。  
**檢查所有專案**  
在所有專案旁邊新增核取記號。 這些專案將會立即在中繼資料瀏覽器中選取。  
  
**取消核取所有專案**  
移除所有專案旁的核取記號。 這些專案將會立即在中繼資料瀏覽器中清除。  
  
**清單視圖模式**  
顯示清單中的篩選項目。  
  
**資料表視圖模式**  
在資料表中顯示篩選的專案。  
  
**只顯示載入的專案**  
切換類別或專案的顯示。 選取此按鈕時，SSMA 會顯示符合篩選準則的所有專案，以及先前載入的專案。 未選取此按鈕時，SSMA 會顯示類別目錄資料夾。  
  
**Filter**  
輸入您要用來篩選項目的字串。 例如，若要尋找專案名稱中包含字串 "ID" 的所有可用專案，請在 [ **篩選** ] 方塊中輸入字串 "id"。  
  
如果專案符合篩選準則，則當您輸入字串時，會顯示類別或專案。 若要查看相符的專案，建議您按一下 [ **只顯示已載入的專案** ] 按鈕。  
  
**清除篩選**  
清除 [ **篩選** ] 方塊。  
  
