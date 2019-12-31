---
title: Updategram 的指導方針和限制（SQLXML）
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9eb717968b191bb7d80f5d68542178bf32734b00
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241301"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML Updategram 的指導方針和限制 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  使用 XML Updategram 時，請記住下列事項：  
  
-   如果您使用 updategram 進行插入作業，且** \<在>之前**和** \<>區塊之後**，則** \<可以省略 before>** 區塊。 相反地，在刪除作業時，可以省略** \<after>** 區塊。  
  
-   ** \<** 如果您使用具有多個** \<>** 的 updategram，以及** \<** 在同步處理 **>\<** 標記中的>區塊之後，必須在** \<>和>組之前，** 指定>區塊** \<>之前** ** \<和之後**的。  
  
-   Updategram 中的更新會套用到 XML 結構描述所提供的 XML 檢視。 因此，若要讓預設的對應成功，您必須在 Updategram 中指定結構描述檔案名稱，或者，如果沒有提供檔案名稱，元素和屬性名稱必須符合資料庫中的資料表和資料行名稱。  
  
-   SQLXML 4.0 要求 Updategram 中的所有資料行值都必須在提供的結構描述 (XDR 或 XSD) 中明確對應，才能構成其子元素的 XML 檢視。 這個行為與舊版的 SQLXML 不同，如果在**sql： relationship**注釋中隱含為外鍵的一部分，則允許在架構中未對應的資料行值。 (請注意，此變更不會影響主索引鍵值傳播到子元素，如果沒有針對子元素明確指定任何值，仍然會發生在 SQLXML 4.0 上。  
  
-   如果您使用 updategram 來修改二進位資料行中的資料（例如[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **image**資料類型），您必須提供對應架構， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]其中必須指定資料類型（例如， **sql： datatype = "image"**）和 XML 資料類型（例如**dt： type = "binhex"** 或**dt： type = "binbase64**）。 您必須在 updategram 中指定 binary 資料行的資料。updategram 會忽略對應架構中指定的**sql： url 編碼**注釋。  
  
-   當您撰寫 XSD 架構時，如果您為 [ **sql：關聯**] 或 [ **sql：] 欄位**注釋指定的值包含特殊字元，例如空白字元（例如，在 "order details" 資料表名稱中），這個值必須以方括弧括住（例如，"[order details]"）。  
  
-   使用 Updategram 時，不支援鏈結關聯性。 例如，如果資料表 A 和 C 透過使用資料表 B 的鏈結關聯性相關聯，嘗試執行 Updategram 時，會發生下列錯誤：  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     即使結構描述和 Updategram 都正確而且格式有效，如果存在鏈結關聯性，則會發生此錯誤。  
  
-   Updategram 不允許在更新期間傳遞**映射**類型資料做為參數。  
  
-   使用 updategram 時，不應該在中** \<>** 使用二進位大型物件（BLOB）類型（例如**text/Ntext**和影像），因為這會包含它們以用於並行存取控制。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 例如，WHERE 子句中會使用 LIKE 關鍵字來比較**text**資料類型的資料行;不過，如果 BLOB 類型的資料大小大於8K，比較將會失敗。  
  
-   **Ntext**資料中的特殊字元可能會因為 BLOB 類型的比較限制而造成 SQLXML 4.0 的問題。 例如，當 updategram 在**Ntext**類型資料行的並行檢查中使用時，使用 "[Serializable]" 的** \<before>** 區塊中的 "[Serializable]" 將會失敗，並出現下列 SQLOLEDB 錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全性考慮](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
