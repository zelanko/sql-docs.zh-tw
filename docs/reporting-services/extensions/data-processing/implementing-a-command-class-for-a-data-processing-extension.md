---
title: "資料處理延伸模組實作命令類別 |Microsoft 文件"
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
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: b601aa43ecce5347f7229999455360be761f3bd3
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>為資料處理延伸模組實作命令類別
  **命令**物件會構成要求，並將它傳遞至資料來源。 命令文字可採用許多不同的語法形式，包括文字與 XML。 如果傳回結果，**命令**物件傳回結果做**DataReader**物件。  
  
 若要建立**命令**類別，實作<xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>。 實作<xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>方法傳回的結果設定為**DataReader**物件。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>方法您**命令**類別應該包括實作採用<xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior>列舉型別做為引數。 如果您將資料處理延伸模組部署到報表設計師，請提供實作以處理 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> 方法中的 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 案例。 僅限結構描述實作是用以提供具有欄位清單的報表設計師。 **DataReader**所傳回物件<xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>方法必須包含類型和名稱資訊欄位，或資料行，在您的結果集中。  
  
 （選擇性） 您**命令**類別可以實作<xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。 這個介面允許實作類別以分析查詢，並在查詢中傳回參數清單。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 介面的功能只能用於報表設計師中。 當您實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 時，允許每當在預覽模式執行報表時，提示報表設計師的使用者所需的參數。 此外，您可以在此檢視中的參數**參數** 索引標籤**資料集**對話方塊。  
  
> [!NOTE]  
>  如果自訂資料處理延伸模組不支援參時，就不應該實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。  
  
 如需範例**命令**類別的實作，請參閱[SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
