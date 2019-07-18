---
title: 註解式轉換為相等的 XSD 結構描述 (SQLXML 4.0) 的 XDR 結構描述 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XDR schemas, converting schemas
- annotated XSD schemas, converting schemas
- XDR to XSD Converter tool [SQLXML]
- XDR schemas [SQLXML], converting
- converting annotated schemas
- mapping schema [SQLXML], conversions
- XSD schemas [SQLXML], converting schemas
ms.assetid: 151c94a8-66d3-4c46-a5ff-a22df456940a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c09f9eff920c11f37f0fd173f6cd612aca6df6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014541"
---
# <a name="converting-annotated-xdr-schemas-to-equivalent-xsd-schemas-sqlxml-40"></a>將註解式 XDR 結構描述轉換為等效 XSD 結構描述 (SQLXML 4.0)
  XML 結構描述定義 (XSD) 語言是 XML-Data Reduced (XDR) 結構描述定義語言的後續版本。 透過在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 中導入的 XSD 支援，系統會假設新的註解式結構描述是使用 XSD 建立的。 SQLXML 4.0 包含 XDR 轉成 XSD 轉換器工具，這項工具是設計來協助您將現有的註解式 XDR 結構描述轉換成對等的 XSD 結構描述。  
  
> [!IMPORTANT]  
>  只有當您想要將註解式 XDR 結構描述轉換成 XSD 以便搭配 SQLXML 4.0 使用時，才應該使用這項工具。 這不是一般用途的 XDR 轉成 XSD 轉換器工具。 在其他環境中使用時，轉換的 XSD 結構描述可能會與原始 XDR 結構描述具有不同的行為。  
  
 如果輸入 XDR 檔案在 XML 宣告內部指定了編碼，這就會成為所產生之 XSD 輸出檔案的編碼。  
  
 轉換器工具 (Cvtschema.exe) 會安裝在 Program Files\SQLXML 4.0\bin 資料夾中，而且它是在命令提示字元中執行。  
  
 下面是一般語法：  
  
```  
cvtschema XDRFileName, [-y], [-w] [-?]  
```  
  
 其中：  
  
 XDRFileName  
 這是要轉換成 XSD 之 XDR 檔案的名稱。 此工具會讀取輸入 XDR 檔案並且在目前的工作目錄中建立 XSD 輸出檔案。 如果輸入檔案具有 .xdr 或 .xml 副檔名，系統就會使用相同的名稱與 .xsd 副檔名來建立輸出 XSD 檔案。 如果輸入檔案具有 .xml 或 .xdr 以外的副檔名 (或者遺漏副檔名)，系統就會使用相同的名稱來建立輸出檔案，並將 .xsd 副檔名附加至輸入檔案名稱。 例如，如果輸入 XDR 檔案名稱為 SampleFile.abc，產生的 XSD 就會儲存成 SampleFile.abc.xsd。  
  
 -y  
 (選擇性) 使用轉換器工具所產生的 XSD 檔案來覆寫現有的 XSD 檔案。 如果沒有指定旗標，此工具會提示您指定是否要覆寫現有的 XSD 檔案，並提供變更輸出檔案名稱的選項。  
  
 -w  
 (選擇性) 傳回在轉換程序中由此工具產生的非嚴重警告。 根據預設，此工具只會針對嚴重錯誤顯示訊息。  
  
 -?  
 傳回您可以使用 `cvtschema` 來指定的選項清單，以及相關說明。  
  
## <a name="see-also"></a>另請參閱  
 [將 XSD 資料類型對應到 XPath 資料類型&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)   
 [XSD 註解&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
  
  
