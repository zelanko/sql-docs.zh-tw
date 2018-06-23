---
title: SSIS 封裝格式 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cfe0e5dc-5be3-4222-b721-fe83665edd94
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: dcb50760bcbe0ce1a4eb01a9a1a2de29565defdf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022414"
---
# <a name="ssis-package-format"></a>SSIS 封裝格式
  在目前的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 版本中，已經對封裝格式 (.dtsx 檔案) 做了重大變更，讓您更輕鬆地讀取此格式及比較封裝。 您也可以更可靠地合併不包含衝突變更或以二進位格式儲存之變更的封裝。  
  
 若要檢視目前的 DTSX 封裝檔案格式，請參閱 [\[MS-DTSX\]: Data Transformation Services Package XML File Format Specification](http://go.microsoft.com/fwlink/?LinkId=233251)([MS-DTSX]：Data Transformation Services 封裝 XML 檔案格式規格)。  
  
 下列清單概述檔案格式變更。 若要檢視這些變更的程式碼範例，請參閱 [SQL Server 2012 中的封裝格式變更](http://go.microsoft.com/fwlink/?LinkId=233255)。  
  
-   已經套用格式化慣例，好讓您更輕鬆地讀取及了解 .dtsx 檔案。  
  
-   此格式更為精簡。 每一個屬性 (Property) 的個別元素已經保存為屬性 (Attribute)，但是 PackageFormatVersion 除外。 屬性 (Attribute) 會依照字母順序列出，而且擁有預設值的屬性 (Property) 將不再保存。 最後，可出現多次的元素現在包含在父元素中。  
  
-   封裝內可由其他物件參考的大多數物件現在擁有封裝 XML 中所定義的 `refId` 屬性。 現在會保存 `refID`，而不會保存歷程識別碼。 歷程識別碼依然會在執行階段內使用，而且載入封裝時會重新產生。  
  
     `refId`值是唯一的字串是可讀取及可了解，相較於 Guid 或整數值。 此字串類似於在舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中用於封裝組態的路徑值。  
  
     如果您要合併的封裝時，兩個版本之間變更`refId`可以用於尋找/取代作業以確保已正確更新所有參考該物件。  
  
-   配置資訊包含在 CData 區段內。  
  
-   註解會以純文字格式保存。 如此可讓您更輕鬆地針對自動產生的文件集擷取資訊。  
  
  