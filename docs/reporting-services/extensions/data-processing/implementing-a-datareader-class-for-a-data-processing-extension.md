---
title: "實作資料處理延伸模組的 DataReader 類別 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: cfd3a6cb38c59b1810d046839cb3be4f0dc9846a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>為資料處理延伸模組實作 DataReader 類別
  **DataReader**物件可讓用戶端從資料來源擷取資料的唯讀、 順向資料流。 為執行查詢，並會儲存在用戶端上的網路緩衝區中，直到您提出要求時，會傳回結果使用**讀取**方法**DataReader**類別。 若要建立**DataReader**類別，實作<xref:Microsoft.ReportingServices.DataProcessing.IDataReader>並選擇性地實作<xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>。 使用**DataReader**物件會增加應用程式的效能藉由擷取資料，只要它是的話，而不是等待查詢傳回，及 （依預設值） 儲存只有一個資料列一次在記憶體中，進而減少系統負荷的整個結果。  
  
 建立的執行個體之後您**命令**類別，建立**DataReader**藉由呼叫物件**Command.ExecuteReader**從資料來源擷取資料列。 **DataReader**實作必須提供兩個基本功能： 順向存取結果集執行的命令和存取資料行類型、 名稱和值內每個資料列。 用戶端使用**讀取**方法**DataReader**從查詢的結果取得資料列的物件。  
  
 在報表設計師中，您**DataReader**物件用來擷取的欄位，以及有關結果集的結構描述資訊清單。 這是藉由實作**GetName**， **GetValue**， **GetFieldType，**和**GetOrdinal**方法<xref:Microsoft.ReportingServices.DataProcessing.IDataReader>介面。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> 介面可讓您提供有關結果集的特定彙總資訊。 如需範例**DataReader**類別的實作，請參閱[SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

