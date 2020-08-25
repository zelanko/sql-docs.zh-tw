---
description: SQL 屬性
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
ms.openlocfilehash: d5c87c5374a0e631b08d355e5f1fc0d7c0862d23
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767407"
---
# <a name="sql-property"></a>SQL 屬性
表示用來取出 [記錄集](../ado-api/recordset-object-ado.md)的查詢字串。  
  
 您可以在 RDS 的設計階段設定 **SQL** 屬性 [。DataControl](./datacontrol-object-rds.md) 物件的物件標記，或在腳本程式碼的執行時間。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>參數  
 *QueryString*  
 包含有效 SQL 資料要求的 **字串** 值。  
  
 *DataControl*  
 代表 RDS 的物件變數 **。DataControl** 物件。  
  
## <a name="remarks"></a>備註  
 一般而言，這是使用資料庫伺服器) 的方言 (的 SQL 語句，例如 `"Select * from NewTitles"` 。 為了確保正確地比對和更新記錄，可更新的查詢必須包含長二進位欄位或計算欄位以外的欄位。  
  
 如果自訂的伺服器端商務物件會抓取用戶端的資料， **SQL** 屬性就是選擇性的。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VBScript) 的 SQL 屬性範例 ](./sql-property-example-vbscript.md)   
 [連接屬性 (RDS) ](./connect-property-rds.md)   
 [ (RDS) 的查詢方法 ](./query-method-rds.md)   
 [ (RDS) 的 Refresh 方法 ](./refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](./submitchanges-method-rds.md)