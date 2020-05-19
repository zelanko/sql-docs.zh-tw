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
author: rothja
ms.author: jroth
ms.openlocfilehash: eb860ed19386b73d90fc26dab8fa96f4b9672a73
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750723"
---
# <a name="sql-property"></a>SQL 屬性
指出用來抓取[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的查詢字串。  
  
 在設計階段，您可以在 RDS 中設定**SQL**屬性[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的物件標記，或在執行時間的腳本程式碼中。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>參數  
 *QueryString*  
 包含有效 SQL 資料要求的**字串**值。  
  
 *DataControl*  
 代表 RDS 的物件變數 **。DataControl**物件。  
  
## <a name="remarks"></a>備註  
 一般而言，這是 SQL 語句（使用資料庫伺服器的方言），例如 `"Select * from NewTitles"` 。 若要確保正確地比對和更新記錄，可更新的查詢必須包含長二進位欄位或計算欄位以外的欄位。  
  
 如果自訂伺服器端商務物件會抓取用戶端的資料，則**SQL**屬性是選擇性的。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL 屬性範例（VBScript）](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [Connect 屬性（RDS）](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Query 方法（RDS）](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh 方法（RDS）](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


