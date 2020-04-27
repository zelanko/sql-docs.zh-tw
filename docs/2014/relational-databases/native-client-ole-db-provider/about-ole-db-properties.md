---
title: 關於 OLE DB 屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- SQL Server Native Client OLE DB provider, properties
- properties [OLE DB]
- property values [SQL Server Native Client]
ms.assetid: 0b36a61e-b542-400d-a3d2-e6f643caf2c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e7c010beaf3aefa4f73314d8576a066dca6a167
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62638070"
---
# <a name="about-ole-db-properties"></a>關於 OLE DB 屬性
  取用者會設定屬性值來要求特定的物件行為。 例如，取用者會使用屬性來指定要由某個資料列集公開的介面。 取用者會取得屬性值來判斷物件 (例如資料列集、工作階段或資料來源物件) 的功能。  
  
 每個屬性 (Property) 都有一個值、類型、描述和讀取/寫入屬性 (Attribute)，而且資料列集屬性 (Property) 還會包含一個指標，表示它是否能夠以逐資料行的方式套用。  
  
 屬性是由 GUID 以及代表屬性識別碼的整數所識別。 屬性集是共用相同 GUID 之所有屬性的集合。 除了預先定義的 OLE DB 屬性集以外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者也會在其中執行提供者特定的屬性集和屬性。 每個屬性都屬於一或多個屬性群組。 屬性群組是套用至特定物件之所有屬性的群組。 某些屬性群組包括初始化屬性群組、資料來源屬性群組、工作階段屬性群組、資料列集屬性群組、資料表屬性群組和資料行屬性群組。 其中每個屬性群組都具有屬性。  
  
 設定屬性值包括：  
  
1.  決定要設定值的屬性。  
  
2.  決定包含已識別之屬性的屬性集。  
  
3.  配置 DBPROPSET 結構的陣列 (針對每個已識別的屬性集配置一個結構)。  
  
4.  針對每個屬性集配置 DBPROP 結構的陣列。 每個陣列中的元素數目就是屬於該屬性集的屬性數目 (在步驟 1 中識別)。  
  
5.  填入每個屬性的 DBPROP 結構。  
  
6.  填入每個屬性集之 DBPROPSET 結構的資訊 (屬性集 GUID、元素數目計數，以及指向對應 DBPROP 陣列的指標)。  
  
7.  呼叫方法來設定屬性並且傳遞 DBPROPSET 結構的計數和陣列。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SQL Server Native Client OLE DB 提供者應用程式](creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [屬性 (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=112207)  
  
  
