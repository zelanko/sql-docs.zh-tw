---
title: SSIS 封裝格式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cfe0e5dc-5be3-4222-b721-fe83665edd94
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f59ed0eee86f17fdda568caa5c1a1dc7252c6d9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055344"
---
# <a name="ssis-package-format"></a>SSIS 封裝格式
  在目前的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]版本中，已經對封裝格式 (.dtsx 檔案) 做了重大變更，讓您更輕鬆地讀取此格式及比較封裝。 您也可以更可靠地合併不包含衝突的變更或變更以二進位格式儲存的封裝。  
  
 若要檢視目前的 DTSX 封裝檔案格式，請參閱[ \[MS-DTSX\]:Data Transformation Services 封裝 XML 檔案格式規格](https://go.microsoft.com/fwlink/?LinkId=233251)。  
  
 下列清單概述檔案格式變更。 若要檢視這些變更的程式碼範例，請參閱 [SQL Server 2012 中的封裝格式變更](https://go.microsoft.com/fwlink/?LinkId=233255)。  
  
-   已經套用格式化慣例，好讓您更輕鬆地讀取及了解 .dtsx 檔案。  
  
-   此格式更為精簡。 每一個屬性 (Property) 的個別元素已經保存為屬性 (Attribute)，但是 PackageFormatVersion 除外。 屬性 (Attribute) 會依照字母順序列出，而且擁有預設值的屬性 (Property) 將不再保存。 最後，可出現多次的元素現在包含在父元素中。  
  
-   封裝內可由其他物件參考的大多數物件現在擁有封裝 XML 中所定義的 `refId` 屬性。 現在會保存 `refID`，而不會保存歷程識別碼。 歷程識別碼依然會在執行階段內使用，而且載入封裝時會重新產生。  
  
     `refId` 值是可讀取及可了解的唯一字串 (相較於 GUID 或整數值)。 此字串類似於在舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中用於封裝組態的路徑值。  
  
     如果您要合併兩個封裝版本之間的變更，則 `refId` 可用於尋找/取代作業，以確保該物件的所有參考都已經正確更新。  
  
-   配置資訊包含在 CData 區段內。  
  
-   註解會以純文字格式保存。 如此可讓您更輕鬆地針對自動產生的文件集擷取資訊。  
  
  
