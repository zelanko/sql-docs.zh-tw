---
title: SQL 屬性 |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4d665e2b2f9ac4d61951da3cccbd16db76127a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727016"
---
# <a name="sql-property"></a>SQL 屬性
表示用來擷取查詢字串[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 您可以設定**SQL**屬性，在設計階段於[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的物件標記，或在指令碼中的執行階段。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>參數  
 *QueryString*  
 A**字串**包含有效的 SQL 資料要求的值。  
  
 *DataControl*  
 物件變數，表示**rds。DataControl**物件。  
  
## <a name="remarks"></a>備註  
 一般情況下，這是 SQL 陳述式 （使用的方言的資料庫伺服器），例如`"Select * from NewTitles"`。 若要確保記錄會比對並準確地更新，可更新的查詢必須包含長二進位欄位或計算的欄位以外的欄位。  
  
 **SQL**屬性是選擇性的如果用戶端的自訂伺服器端商務物件會擷取的資料。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL 屬性範例 (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [連接屬性 (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [查詢方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


