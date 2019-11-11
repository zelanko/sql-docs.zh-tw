---
title: 尋找搜尋屬性的屬性集 GUID 與屬性整數識別碼 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], configuring
ms.assetid: 7db79165-8bcc-4be6-8d40-12d44deda79f
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 94a7ad079b94d9bc34e5b0e7f7ad55393d8f5de5
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73638050"
---
# <a name="find-property-set-guids-and-property-integer-ids-for-search-properties"></a>尋找搜尋屬性的屬性集 GUID 與屬性整數識別碼
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主題將討論如何取得將屬性加入至搜尋屬性清單，使全文檢索搜尋能夠進行搜尋所需的值。 這些值包括文件屬性的屬性集 GUID 和屬性整數識別碼。  
  
 IFilter 從二進位資料 (也就是儲存在 **varbinary**、**varbinary(max)** (包括 **FILESTREAM**) 或 **image** 資料類型資料行中的資料) 擷取的文件屬性可供全文檢索搜尋使用。 若要使擷取的屬性可搜尋，則必須手動將屬性加入至搜尋屬性清單。 同時，搜尋屬性清單必須與一個或多個全文檢索索引產生關聯。 如需詳細資訊，請參閱 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
 在屬性清單中加入可用屬性之前，您必須先找到有關屬性的兩項資訊：  
  
-   屬性的屬性集 GUID。  
  
-   屬性的整數識別碼。  
  
 (您將屬性加入至屬性清單時，也要提供名稱和描述。 不過，您不必使用屬性的正式名稱和描述)。  
  
 本主題描述尋找可用屬性相關資訊的常用方法，尤其是有關 Microsoft 所定義的屬性。 如需有關協力廠商已定義屬性的詳細資訊，請參閱協力廠商文件集或連絡該廠商。  
  
##  <a name="wellknown"></a> 尋找廣泛使用之已知 Microsoft 屬性的詳細資訊  
 Microsoft 定義了數百個文件屬性可用於許多內容，但是每一種檔案格式只會使用其中一小部分可用屬性。 常用的 Windows 屬性包括少數泛型屬性。 下表將顯示已知泛型屬性的部分範例。 下表顯示了已知名稱、Windows 正式名稱 (根據 Microsoft 發行的屬性描述)、屬性集 GUID、屬性整數識別碼和簡短說明。  
  
|已知名稱|Windows 正式名稱|屬性集 GUID|整數識別碼|Description|  
|----------------------|----------------------------|-----------------------|----------------|-----------------|  
|Authors|**System.Author**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|4|給定項目的一位或多位作者。|  
|Tags|**System.Keywords**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|5|指派給項目的關鍵字集合 (也稱為標記)。|  
|類型|**System.PerceivedType**|28636AA6-953D-11D2-B5D6-00C04FD918D0|9|以正式類型為基礎的認知檔案類型。|  
|Title|**System.Title**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|2|項目的標題。 例如文件的標題、郵件的主旨、相片的標題或音樂曲目的名稱。|  
  
 為了鼓勵檔案格式的一致性，Microsoft 已經針對許多文件類別識別了常用且高優先順序的文件屬性子集。 這些類別包括通訊、連絡人、文件、音樂檔案、圖片和視訊。 如需每個類別目錄前幾項排名屬性的詳細資訊，請參閱 Windows Search 文件集中的 [system-defined properties for custom file formats](https://go.microsoft.com/fwlink/?LinkId=144336) (自訂檔案格式的系統定義屬性)。  
  
 特定檔案格式可能會實作三種類型的屬性：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]定義的泛型屬性。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]定義的特定類別目錄屬性。  
  
-   軟體廠商定義的自訂、應用程式專用屬性。  
  
##  <a name="filtdump"></a> 使用 FILTDUMP.EXE 尋找可用屬性的詳細資訊  
 若要了解已安裝之 IFilter 所找到和擷取的屬性，您可以安裝並執行 **filtdump.exe** 公用程式 (屬於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK 的一部分)。  
  
 您可以從命令提示字元執行 **filtdump.exe** ，並提供單一引數。 此引數是個別檔案的名稱，而該檔案具有已安裝 IFilter 的檔案類型。 此公用程式顯示文件中 IFilter 所找到之所有屬性的清單，還包含其屬性集 GUID、整數識別碼和其他資訊。  
  
 如需安裝此軟體的相關資訊，請參閱 [Microsoft Windows SDK for Windows 7 和 .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=8279)。 在您下載並安裝 SDK 之後，請查看下列資料夾中是否有 filtdump.exe 公用程式。  
  
-   針對 64 位版本，請查看 `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\x64`。  
  
-   針對 32 位版本，請查看 `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin`。  
  
##  <a name="propdesc"></a> 從 Windows 屬性描述尋找搜尋屬性的值  
 若為已知的 Windows 搜尋屬性 (Property)，您可以從屬性 (Property) 描述 ( **propertyDescription** ) 的 **formatID** 和**propID**屬性 (Attribute) 取得您需要的這項資訊。  
  
 下列範例將顯示一般 Microsoft 屬性描述的相關部分 (以 `System.Author` 屬性為例)。 `formatID` 屬性 (Attribute) 會指定屬性 (Property) 集 GUID `F29F85E0-4FF9-1068-AB91-08002B27B3D9`，而 `propID` 屬性 (Attribute) 會指定屬性 (Property) 整數識別碼 `4.` 。請注意， `name` 屬性 (Attribute) 會指定 Windows 正式屬性 (Property) 名稱 `System.Author` (這個範例省略了屬性描述中不相關的部分)。  
  
```  
.  
propertyDescription  
name = System.Author  
...  
formatID = F29F85E0-4FF9-1068-AB91-08002B27B3D9  
propID = 4  
...  
```  
  
 如需此屬性的完整描述，請參閱 Windows Search 文件集中的 [System.Author](https://go.microsoft.com/fwlink/?LinkId=144337) 。  
  
 如需 Windows 屬性的完整清單，請參閱同樣在 Windows Search 文件集中的 [Windows Properties](https://go.microsoft.com/fwlink/?LinkId=215013)Windows 屬性)。  
  
##  <a name="examples"></a> 將屬性加入至搜尋屬性清單  
 下列範例示範如何將屬性加入至搜尋屬性清單。 此範例會使用 [ALTER SEARCH PROPERTY LIST](../../t-sql/statements/alter-search-property-list-transact-sql.md) 陳述式將 `System.Author` 屬性加入名為 `PropertyList1`的搜尋屬性清單，並且為屬性提供使用者易記名稱 `Author`。  
  
```  
ALTER SEARCH PROPERTY LIST PropertyList1   
  ADD 'Author'  
    WITH (  
          PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',  
          PROPERTY_INT_ID = 4,   
          PROPERTY_DESCRIPTION = 'System.Author - the author or authors of the item'   
         )  
GO  
```  
  
 如需建立搜尋屬性清單並將它與全文檢索索引產生關聯的詳細資訊，請參閱 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [設定及管理搜尋的篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
  
