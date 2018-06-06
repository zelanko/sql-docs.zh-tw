---
title: SQL 屬性 |Microsoft 文件
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5ddbfa6b69f4859f61130e8ec1c9b758c40cf64
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sql-property"></a>SQL 屬性
表示用來擷取查詢字串[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 您可以設定**SQL**屬性在設計階段於[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的物件標記，或在指令碼中的執行階段。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>參數  
 *QueryString*  
 A**字串**包含有效的 SQL 資料要求的值。  
  
 *DataControl*  
 物件變數，表示 **.RDSDataControl**物件。  
  
## <a name="remarks"></a>備註  
 一般情況下，這是 SQL 陳述式 （使用的方言的資料庫伺服器），例如`"Select * from NewTitles"`。 若要確保記錄會比對，並正確地更新，可更新的查詢必須包含二進位長的欄位或計算的欄位以外的欄位。  
  
 **SQL**屬性如果設定是選擇性的自訂伺服器端的商務物件擷取資料的用戶端。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL 屬性範例 (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [屬性 (RDS) 連接](../../../ado/reference/rds-api/connect-property-rds.md)   
 [查詢方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [重新整理方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


