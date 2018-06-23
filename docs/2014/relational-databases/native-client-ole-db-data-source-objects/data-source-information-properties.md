---
title: 資料來源資訊屬性 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 980e7ea889cc8c95828b4c704748aa6dc2552359
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134619"
---
# <a name="data-source-information-properties"></a>資料來源資訊屬性
  在提供者專用的屬性集 DBPROPSET_SQLSERVERDATASOURCEINFO 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義下列資料來源資訊屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|類型：VT_BOOL<br /><br /> R/W：讀取<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述：用於判斷是否支援資料行定序。<br /><br /> VARIANT_TRUE：支援資料行層級定序。<br /><br /> VARIANT_FALSE：不支援資料行層級定序。|  
|SSPROP_UNICODELCID|類型：VT_I4 R/W：讀取<br /><br /> 描述：Unicode 地區設定識別碼。<br /><br /> 這是用於 Unicode 資料排序的地區設定。|  
|SSPROP_UNICODECOMPARISONSTYLE|類型：VT_I4 R/W：讀取<br /><br /> 描述：Unicode 比較樣式。<br /><br /> 用於 Unicode 資料排序的排序選項。|  
  
 在提供者專屬的屬性集 DBPROPSET_SQLSERVERSTREAM 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義以下額外的屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|類型：VT_BSTR R/W：讀取/寫入<br /><br /> 描述：FOR XML 查詢的結果可能不是格式正確的文件。 指定此屬性時，結果 ' 選取... for XML' 查詢會包裝在提供此屬性以傳回格式正確的 XML 文件的根標記。 如果在瀏覽器中執行查詢，載入結果時，它可能會使瀏覽器顯示剖析器錯誤。 為避免這個錯誤，SQL ISAPI 支援關鍵字 ROOT。 此關鍵字會對應至 SSPROP_STREAM_XMLROOT 屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件&#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  