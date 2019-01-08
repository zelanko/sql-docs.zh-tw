---
title: 為資料處理延伸模組實作 DataReader 類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8815a136a80ad6ba3ae838d54e50e7932435b3ac
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363290"
---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>為資料處理延伸模組實作 DataReader 類別
  **DataReader** 物件允許用戶端從資料來源擷取唯讀、順向的資料流。 執行查詢時會傳回結果，並一直儲存於用戶端上的網路緩衝區中，直到您使用 **DataReader** 類別的 **Read** 方法要求它們為止。 若要建立 **DataReader** 類別，請實作 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 並選擇性地實作 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>。 使用 **DataReader** 物件可以提高應用程式的效能，方法是在資料可用時立即擷取它，而不是等待傳回查詢的整個結果，以及 (依預設) 一次只將一個資料列儲存到記憶體中，進而減少系統負擔。  
  
 在建立 **Command** 類別的執行個體之後，可以呼叫 **Command.ExecuteReader** 從資料來源擷取資料列來建立 **DataReader** 物件。 **DataReader** 實作必須提供兩個基本功能：順向存取執行命令所擷取的結果集，並存取每個資料列中的資料行類型、名稱和值。 用戶端使用 **DataReader** 物件的 **Read** 方法，從查詢結果取得資料列。  
  
 在報表設計師中，**DataReader** 物件是用以擷取欄位清單以及有關結果集的結構描述資訊。 這是透過實作 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 介面的 **GetName**、**GetValue**、**GetFieldType** 和 **GetOrdinal** 方法來完成。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> 介面可讓您提供有關結果集的特定彙總資訊。 如需範例 **DataReader** 類別實作，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../reporting-services-extensions.md)   
 [實作資料處理延伸模組](implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
