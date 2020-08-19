---
description: Record (ADO for Visual C++ 語法)
title: 記錄 (ADO for Visual C++ 語法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- Record collection [ADO], ADO for Visual C++ syntax
ms.assetid: c4ce8532-a4d8-4f74-9488-9389b6695958
author: rothja
ms.author: jroth
ms.openlocfilehash: be4addb8a8a774a8128e721de9052ca5351959f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442520"
---
# <a name="record-ado-for-visual-c-syntax"></a>Record (ADO for Visual C++ 語法)
## <a name="methods"></a>方法  
  
```  
Cancel(void)  
Close(void)  
CopyRecord(BSTR Source, BSTR Destination, BSTR UserName, BSTR Password, CopyRecordOptionsEnum Options, VARIANT_BOOL Async, BSTR *pbstrNewURL)  
DeleteRecord(BSTR Source, VARIANT_BOOL Async)  
GetChildren(_ADORecordset **ppRSet)  
MoveRecord(BSTR Source, BSTR Destination, BSTR UserName, BSTR Password, MoveRecordOptionsEnum Options, VARIANT_BOOL Async, BSTR *pbstrNewURL)  
Open(VARIANT Source, VARIANT ActiveConnection, ConnectModeEnum Mode, RecordCreateOptionsEnum CreateOptions, RecordOpenOptionsEnum Options, BSTR UserName, BSTR Password)  
```  
  
## <a name="properties"></a>屬性  
  
```  
get_ActiveConnection(VARIANT *pvar)  
put_ActiveConnection(BSTR bstrConn)  
putref_ActiveConnection(_ADOConnection *Con)  
get_Fields(ADOFields **ppFlds)  
get_Mode(ConnectModeEnum *pMode)  
put_Mode(ConnectModeEnum Mode)  
get_ParentURL(BSTR *pbstrParentURL)  
get_RecordType(RecordTypeEnum *pType)  
get_Source(VARIANT *pvar)  
put_Source(BSTR Source)  
putref_Source(IDispatch *Source)  
get_State(ObjectStateEnum *pState)  
```  
  
## <a name="see-also"></a>另請參閱  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
