---
title: 為資料處理延伸模組實作命令類別 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2093aad82661133944227dbd0458b66cfb19da94
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50028717"
---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>為資料處理延伸模組實作命令類別
  **Command** 物件會構成要求，並將它傳遞到資料來源。 命令文字可採用許多不同的語法形式，包括文字與 XML。 如果傳回結果，**Command** 物件會傳回結果以作為 **DataReader** 物件。  
  
 若要建立 **Command** 類別，請實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>。 實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 方法以傳回結果集作為 **DataReader** 物件。 **Command** 類別的 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 方法應該包括實作，它需要 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> 列舉作為引數。 如果您將資料處理延伸模組部署到報表設計師，請提供實作以處理 <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> 方法中的 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 案例。 僅限結構描述實作是用以提供具有欄位清單的報表設計師。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> 方法傳回的 **DataReader** 物件，需要在結果集中包含欄位或是資料行中的類型與名稱資訊。  
  
 (選擇性) 您的 **Command** 類別可以實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。 這個介面允許實作類別以分析查詢，並在查詢中傳回參數清單。 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 介面的功能只能用於報表設計師中。 當您實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> 時，允許每當在預覽模式執行報表時，提示報表設計師的使用者所需的參數。 此外，您可以在 [資料集] 對話方塊的 [參數] 索引標籤中檢視參數。  
  
> [!NOTE]  
>  如果自訂資料處理延伸模組不支援參時，就不應該實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>。  
  
 如需範例 **Command** 類別實作，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
