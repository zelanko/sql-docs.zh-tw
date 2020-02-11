---
title: ADO 物件和介面 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5ecc6de67defb2366bf208c38bd2de5bff643e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920902"
---
# <a name="ado-objects-and-interfaces"></a>ADO 物件和介面
這些物件之間的關聯性會以[ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)表示。  
  
 每個物件都可以包含在其對應的集合中。 例如，[錯誤](../../../ado/reference/ado-api/error-object.md)物件可以包含在[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合中。 如需詳細資訊，請參閱[ADO 集合](../../../ado/reference/ado-api/ado-collections.md)或特定集合主題。  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|用來從 ADOCommand 物件中取出基礎 OLEDB 命令。|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|從 C/c + + 應用程式中的 OLE DB **Row**物件，建立 ADO**記錄**物件。|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|從 C/c + + 應用程式中的 OLE DB 資料列**集**物件，來建立 ADO**記錄集**物件。|  
|[ADOStreamConstruction 介面](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|從 C/c + + 應用程式中的 OLE DB **IStream**物件，來建立 ADO**資料流程**物件。|  
|[命令](../../../ado/reference/ado-api/command-object-ado.md)|定義您想要針對資料來源執行的特定命令。<br /><br /> **命令**物件不安全，無法進行腳本處理。|  
|[[連接]](../../../ado/reference/ado-api/connection-object-ado.md)|表示與資料來源的開啟連接。<br /><br /> **連接**物件可安全地進行腳本處理。|  
|[IDSOShapeExtensions 介面](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|取得圖形提供者的基礎 OLEDB 資料來源物件。|  
|[錯誤](../../../ado/reference/ado-api/error-object.md)|包含有關與提供者的單一作業相關之資料存取錯誤的詳細資訊。<br /><br /> **錯誤**物件對腳本而言是不安全的。|  
|[欄位](../../../ado/reference/ado-api/field-object.md)|表示具有 common 資料類型的資料行。|  
|[參數](../../../ado/reference/ado-api/parameter-object.md)|根據參數化查詢或預存程式，表示與**命令**物件相關聯的參數或引數。<br /><br /> **參數**物件不安全，無法進行腳本處理。|  
|[屬性](../../../ado/reference/ado-api/property-object-ado.md)|表示由提供者定義之 ADO 物件的動態特性。|  
|[記錄](../../../ado/reference/ado-api/record-object-ado.md)|表示**記錄集**的資料列，或檔案系統中的目錄或檔案。 **記錄**物件可安全地進行腳本處理。|  
|[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)|表示基表中的記錄集或已執行命令的結果。 **記錄集**物件隨時只會參考集合中的單一記錄做為目前的記錄。<br /><br /> **記錄集**物件可安全地進行腳本處理。|  
|[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)|表示資料的二進位資料流程。<br /><br /> **資料流程**物件可安全地進行腳本處理。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 B： ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
